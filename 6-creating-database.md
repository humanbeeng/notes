## Creating a database

Inside data/local folder

We shall create a new Database **abstract class** which inherits its functionalities from Room Database

```java
@Database(
	entities = [WordInfoEntities::class],
	version
)

abstract class WordInfoDatabase : RoomDatabase(){
	// Specify the DAO which operates on this database

	abstract val dao : WordInfoDao;
}

```

Room will take care of the rest for us

