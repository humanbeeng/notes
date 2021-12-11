# API Layer

Let's start from bottom all the way up

We know that we will be fetching the word info from an API and displaying to our screen

Inside the feature_dictionary/data/remote/ folder, create a interface called DictionaryApi.kt


```java

interface DictionaryApi{
	@GET("/api/v2/entries/en/{word})
	suspend fun getWordInfo(@PATH("word") word : String) : List<WordInfo>;
}

```
This is the Retrofit implementation, Retrofit is capable of returning List of items


Now that we have the handler for the API request, let's have some data classes which represents the responses from the request.

We can do this the easy way where, if we have the JSON response readily available, we can make use of JSON to Kotlin Data class plugin in IntelliJ


It creates DTO classes from the JSON responses

Kindly make sure that types are proper of each members


