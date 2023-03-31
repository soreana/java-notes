# Difference between new HashMap<>(int) and HashMap.newHashMap(int)

### Summary

When we create a hash map using `new HashMap<>(180)`, java resize the HashMap when it reaches the size of `135` = 180*0.75 . It happens because of the `0.75` load factor. In Java 19, we can use `newHashMap(180)`
 static method that creates HashMap with `240`=180/0.75 elements which resized at a size of `180`.

### The Complete Article

The following lines are copied from [this article](https://blogs.oracle.com/javamagazine/post/java-19-enhancements-fixes-deprecations) about the new features in Java 19.


If you want to create an ArrayList of 180 elements, you could write the following code:

```java
List<String> list = new ArrayList<>(180);
```

The underlying array, the ArrayList, is allocated directly for 180 elements and does not have to be enlarged several times as you insert the 180 elements.

Similarly, you might try to create a HashMap with 180 preallocated mappings as follows:

```java
Map<String, Integer> map = new HashMap<>(180);
```

Intuitively, you would think that this new HashMap offers space for 180 mappings. However, it does not! This happens because the HashMap has a default load factor of 0.75 when it is initialized. This indicates that the HashMap gets rebuilt (also called rehashed) with double the size as soon as it is 75% filled. Thus, the new HashMap is initialized with a capacity of 180 and can hold only 135 (180 × 0.75) mappings without being rehashed.

Therefore, to create a HashMap for 180 mappings, calculate the capacity by dividing the number of mappings by the load factor: 180 ÷ 0.75 = 240. So, a HashMap for 180 mappings would be created as follows:

```java
// for 180 mappings: 180 / 0.75 = 240
Map<String, Integer> map = new HashMap<>(240);
```

Java 19 makes it easier to create a HashMap that has the required mappings without fiddling with load factors by using the new static factory method newHashMap(int).

```java
Map<String, Integer> map = HashMap.newHashMap(180);
```

Look at the source code to see how it works.

```java
public static <K, V> HashMap<K, V> newHashMap(int numMappings) {
    return new HashMap<>(calculateHashMapCapacity(numMappings));
}

static final float DEFAULT_LOAD_FACTOR = 0.75f;

static int calculateHashMapCapacity(int numMappings) {
    return (int) Math.ceil(numMappings / (double) DEFAULT_LOAD_FACTOR);
}
```

Similar labor-saving static factory methods have been created in Java 19. Here’s the complete set.


1. HashMap.newHashMap

2. LinkedHashMap.newLinkedHashMap

3. WeakHashMap.newWeakHashMap

4. HashSet.newHashSet

5. LinkedHashSet.newLinkedHashSet
