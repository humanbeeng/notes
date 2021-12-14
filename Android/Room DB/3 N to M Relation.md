# N to M Relation

Suppose a Owner can have multiple Dogs and Dog can have multiple Owners. This relation is referred to as N to M relation.

> Goal : To retrieve list of all owners with their dogs -> List<OwnerWithDogs>

```json
// List<OwnerWithDogs>
[
  {
    "Owner": {},
    "Dog": [{}, {}]
  },
  {
    "Owner": {},
    "Dog": [{}, {}]
  }
]
```

Now that we have mentioned that dogs can multiple owners and owners can have multiple dogs, keep in mind that we cannot store duplicate values of dogs itself corresponding to different owners since dogId will be the same for this duplicate entries and this dogId is also the primary key -> hence we cannot store duplicate entries of primary keys. This applies same for owners as well. We cannot have owner with dog1 and same owner with dog1 in a single table, since ownerId will remain the same.

To overcome this, we need to define a new CrossRef table which maps ownerId with dogId. This table shall have two primary keys = ["ownerId", "dogId"].

> A table should have at least one primary key. Hence, we can have multiple primary keys as well.

```kotlin

@Entity(primaryKeys = ["ownerId", "dogId"])
data class DogOwnerCrossRef(
	val dogId : Long,
	val ownerId : Long
)

```

> Note : The above mentioned class is actually a new table (Entity)

We still don't have the output which is to have a List containing Owners along with their Dogs.
We shall define this output as List<OwnerWithDogs>

In order to get the `Dogs` field(List) inside the OwnerWithDogs, we need to specify Room that in order to get this, you need to reference our `DogOwnerCrossRef`.

```kotlin

data class OwnerWithDogs(
	@Embedded val owner : Owner,

	@Relation(parentColumn = "ownerId", entityColumn = "dogId", associateBy = Junction(DogOwnerCrossRef::class))
	val dogs : List<Dog>
)


```

### Dao

```kotlin
@Transaction
@Query("SELECT \* FROM OWNER")
suspend fun getOwnersWithDogs() : List<OwnerWithDogs>

```
