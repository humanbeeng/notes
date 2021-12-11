## DTOs and Models

Our request handler will send in responses which contains necessary information as per the request.

Consider a scenario where the response contains data which is more than needed to display in the UI. In this case, we need to filter out the data which we want to display it to the users. 

Here comes Models, Models are defined inside the domain layer. These contains the relevant data to move up to the presentation layer.


In order to filter out the necessary data, we need to define mapper functions inside Data classes of DTO



```java
data class WordInfoDto(
	val meanings : List<MeaningDto>,
	val origin : String, 
	.
	.
	.
	){
		fun toWordInfo() : WordInfo{
			return WordInfo(val meanings = meanings.map(
				it.toMeaning()
			),
			val origin = origin,
			val phonetic = phonetic
			)
		}
}

```

We can define the WordInfo class with only the necessary fields and use the mapper whenever we need access to this Dto to conform with the model, just like we are calling meanings.map(it.toMeaning()). Here we are essentially storing List<Meaning> inside of WordInfo class instead of List<MeaningDto>.



