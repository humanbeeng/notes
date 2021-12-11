## Storing things inside database

Entities : The things we store inside the database are called Entities. Example : Person, Product  ---> Stored in Tables

Tables define the attributes of the entities which make up for the uniqueness of each entity.

Inside the data/local/entities folder, create a new Data class 




Since we will be caring about the WordInfo and do not care whether we fetch it from local or remote. It makes sense to make sure the entities match up with the Dto defined in remote layer to maintain consistency in the data passed as models in domain layer.


```java
@Entity
data class WordInfoEntity(
	val word : String, 
	val phonetic : String, 
	val origin : String,
	val meanings : List<Meaning>
	@PrimaryKey id : Int? : null
){
	fun toWordInfo(){
		return WordInfo(val meanings = meanings.map(
				it.toMeaning()
			),
			val origin = origin,
			val phonetic = phonetic
			)
	}
}

```


We are storing only the WordInfo inside the database as a whole(WordInfo already contains / wraps the other Dto's and it does not make sense to store it explicitly in db).


