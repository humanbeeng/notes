# One to One Relation
Example : A Owner can have only one dog AND that dog can have only one Owner.


```kotlin

@Entity
data class Owner(
	@PrimaryKey ownerId : Long, 
	val name : String
)

```


```kotlin

@Entity
data class Dog(
	@PrimaryKey dogId : Long,
	val dogOwnerId : Long, 
	val name : String,
	val breed : String
)

```

> GOAL : To retrieve a list of Dogs and their Owners

ie -> `List<DogAndOwner>`

We can define this relation in a separate data class
>Note that Dog class contains the dogOwnerId, but Owner does not contain dogId, although if it were inverted(owner containing dogId but Dog not containing dogOwnerId) it wont make any difference, but, we need to be careful when we are querying with relation to each other. Like here, we are fetching List of Dog and their owners. Our relation class should have Owner object embedded as a whole, but, Dog class must be the primary driver, ie, our Relation should be resolved inside Dog class itself.

```kotlin

data class DogAndOwner{
	@Embedded val owner : Owner,

	@Relation(parentColumn = "ownerId", entityColumn = "dogOwnerId")
	val dog : Dog
}


```
> Note that the above data class is not an entity, rather, just a data class -> remember the diamond symbol in the diagram. This data class corresponds to the diamond.

## Dao 

```kotlin

@Transaction
@Query("SELECT * FROM Owner")
fun getDogsAndOwners() : List<DogAndOwner>

```