# One to many relation

- Use 'with' when defining relation data class. Ex : SchoolWithStudents
- parentColumn refers to the actual source column, entityColumn holds reference to the values of parentColumn, but not the actual data itself. 
- We need to define the another member which holds the result of the relation itself. 

```kotlin
data class SchoolWithStudents(
	@Embedded val school : School,
	@Relation(
		parentColumn : "schoolName",
		entityColumn : "schoolName,
	)
	val students : List<Student>
)
```


### Inside Dao
```kotlin

@Transaction -> Thread safety - Atomicity of the query
@Query("SELECT * FROM school WHERE schoolName = :schoolName")
suspend fun getSchoolWithStudents(schoolName : String)  : List<Student>


```