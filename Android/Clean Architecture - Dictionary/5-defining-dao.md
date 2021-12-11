## Defining DAO

DAO - Data Access Object : These are the interfaces which performs database operations.


```java
@Dao
interface WordInfoDao{

	@Insert(onConflict = onConflictStrategy.REPLACE)
	suspend fun insertWordInformation(information : List<WordInfoEntity>)

	@Query("DELETE from wordinfo where word IN (:word)")
	suspend fun deleteWordInformation(words : List<String>)


	@Query("SELECT * from wordinfo where word LIKE '%'|| :word || '%'")
	suspend fun fetchWordInfo(word : String)
}
```

Remember that we have a field called word inside WordInfoEntity and we can use it to delete and fetch information about the word itself