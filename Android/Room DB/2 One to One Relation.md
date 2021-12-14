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