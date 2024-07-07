<center><h1>Arguments</h1></center>
<center><p>Command argument declaration and options.</p></center>

---

# Complex arguments
By default, other more complex arguments are also allowed, for example `Collections`, like `List` or `Set`.  

# Collections
Collections are also type safe, meaning if you do `List<Integer>` that means any argument that is *not* a number will be `null`, for example:  
`/foo bar 1 2 3 hello 4 5` -> `[1, 2, 3, null, 4, 5]`.  
Collections by default are **only** allowed as the last argument, for example:
```java
void execute(Sender sender, int number, List<String> args);
```
With one exception being a split argument.

## Split argument
A split argument is a collection that is annotated by `@Split`, example:  
Given the command `/foo bar diamond,iron_ingot,stone,grass_block 5`, can be declared as:  
```java
void execute(Sender sender, @Split(",") List<Material> materials, int amount) {
    println(materials); // Would print [DIAMOND, IRON_INGOT, STONE, GRASS_BLOCK]
}
```

## Join argument
The same way you can split a string into a collection, you can also join a list of arguments into a single string.  
This however can only be used as the last argument of the command.  
Command example: `/foo bar 5 hello there people`.
```java
void excecute(Sender sender, int number, @Join(", ") String message) {
    println(message); // Would print "hello, there, people"
}
```
