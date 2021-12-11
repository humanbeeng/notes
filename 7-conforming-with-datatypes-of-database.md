## Conforming datatypes


When we want to store complex data types (like List<Meaning>) SQL databases doesn't support this type of data to be stored. Either we have to create a new table called Meaning which contains all the fields from the Meaning class as String and others and then use one-to-many or other suitable relation to store the List<Meaning> inside the WordInfo table.

Instead, to avoid the complexity of such scenario, this is a very simple use case and hence we are just going to parse the data class as String using GSON or other JSON parser and convert the data class to String and store it inside the meaning field. We can also deserialize the String using JSON Parsers as well(When we want to use the data inside the app)

Let's create our JSON Parser functionality

Inside our data layer, create a new folder called util

Let's create a new JSON Parser which can Serialize and Deserialize the data given to it(Use of Generics)

Note : We could've use GSON directly to serialize the data and then store or use it. But when we want to change our parser from GSON to, say, Kotlin Serializer, if this happens we have to make changes to places wherever GSON was used directly and this is not clean. 

Instead focus on the functionality requirement : 
We want to have a Service which can serialize and deserialize the data when needed. 

We can define this service abstractly as JSONParser and hand out to functionality to other places which require JSONParser


This JSONParser can further implement from any Parser, and the other classes need not worry about the changes at all as long as the service it provides works. This also leads to flexible code where we can make changes to a single place.


```java
import java.reflect.Type

interface JSONParser{ 

	fun <T> fromJSONtoOriginalType(jsonString : String, type : Type) : T?

	fun <T> fromOriginalTypeToJSON(object : T, type : Type ) : String?
}

```

Making it nullable in case something goes wrong we return null


Now comes the actual implementation


Inside the same folder, ie, feature_dictionary/data/util , create a new implementation class

```java

class JSONParserImpl(
	private val gson : Gson
) : JSONParser {

	override fun <T> fromJSONtoOriginalType(jsonString : String, type : Type): T{
		return gson.fromJSON(jsonString, type)
	}

	override fun <T> fromOriginalTypeToJSON(object : t, type : Type) : String?{
		return gson.toJSON(object, type)
	}


}

```