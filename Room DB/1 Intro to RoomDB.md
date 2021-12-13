## Intro to Room DB

Made up of three components:

1. Entities
2. DAO
3. Database

### Entities
Entities are entities in real world. Basically tables, for example : Person, Product. These are represented as tables in SQL Database.

```java

@Entity(table_name = "users")
data class User(
	@PrimaryKey(autoGenerate = true)
	val id : Int,
	val name : String, 
	val age : Int
)

```

### DAO
Data Access Object -> It is an interface defining methods which interact with the tables.

`@Query`, `@Insert` are the Annotations given to the methods 

```java

@Dao
interface UserDao{

	@Insert(onConflict = onConflictStrategy.IGNORE )
	suspend fun addUser(newUser : User)

	@Query("SELECT * FROM users ORDER BY id ASC")
	suspend fun fetchAllUsers() : LiveData<List<User>>

}


```