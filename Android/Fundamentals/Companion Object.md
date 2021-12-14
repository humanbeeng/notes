# Companion Object

# Companion Object

We are familiar with classes and its members. Let's have a class `Multiplier` which multiplies a given number by a certain factor.

This multiplierFactor is a member of the class and has nothing to do with the instance of the Multiplier class.

This multiplierFactor can be access (modified too, if not val) through Multiplier.multiplierFactor, as compared to creating an instance of Multiplier and then accessing the multiplierFactor via its object.

> These are called static members of the class

In Kotlin we don't have static keyword, instead, we define all the members inside a companion object which resides inside the class itself.

```kotlin

class Multiplier{
	companion object{
		var multiplierFactor : Int = 10

		fun printHello() = println("Hey there !")
	}
}


fun main(args : Array<String>){
	print(Multiplier.multiplierFactor)
}

```
