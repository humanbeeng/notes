# One to many relation

- Use 'with' when defining relation data class. Ex : SchoolWithStudents
- parentColumn refers to the actual source column, entityColumn holds reference to the values of parentColumn, but not the actual data itself. 
- We need to define the another member which holds the result of the relation itself. 


**Example scenario** :
A Owner can have multiple dogs and we need to retrieve list of all dogs of a particular Owner.

Consider that we have Owner and Dogs class: 
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


> Goal : To display list of Owners with their Dogs
This relation can be defined as `OwnerWithDogs`

```kotlin

data class OwnerWithDogs(
	@Embedded val owner : Owner,

	@Relation(parentColumn = "ownerId", entityColumn = "dogOwnerId")
	val dogs : List<Dog>
)

```

### Dao

@Transaction
@Query("SELECT * FROM Owner")
suspend fun getDogsAndOwners() : List<OwnerWithDogs>
