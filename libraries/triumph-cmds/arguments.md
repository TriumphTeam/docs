<center><h1>Arguments</h1></center>
<center>
<p>Command arugment declaration and options.</p>
</center>

---

# Concept
The concept of arguments in the library are based on parameters, each parameter declared in the method will be a command argument.

# Sender
The first parameter of the command method **must** always be a sender. You can read more about the sender [here](/).

# Creating a command with arguments
Let's create the following command `/give item diamond 5`. Where `give` is the command, `item` is the sub command, `diamond` is an argument of type `Material` and `5` is the amound or an `int`.
```java
@Command("give")
class MyClass extends BaseCommand {

    @SubCommand("item")
    public void execute(Sender sender, Material material, int amount) {
        sender.sendMessage("The selected material was: " + material); // Will send "diamond"
        sender.sendMessage("The amount was: " + amount); // Will send "5"
    }
}
```
It is as simple as that to have arguments for your command.

# Simple arguments
By default the library adds many argument types.

**Common:**
* `short`/`Short`
* `int`/`Integer`
* `long`/`Long`
* `float`/`Float`
* `double`/`Double`
* `boolean`/`Boolean`
* `String`
* `Enums` - Any type of enums, for example `Material`.

Aditionally each platform also adds a few default types.

**Bukkit**
* `Material` - Overriden from normal enums to use `matchMaterial` instead of `valueOf`.
* `Player`
* `World`

**JDA**
* `User`
* `Member`
* `TextChannel`
* `VoiceChannel`
* `Role`

# Complex arguments
By default other more complex aguments are also allowed, for example `Collections`, like `List` or `Set`.  

## Collections
Collections are also type safe, meaning if you do `List<Integer>` that means any argument that is *not* a number will be `null`, for example:  
`/foo bar 1 2 3 hello 4 5` -> `[1, 2, 3, null, 4, 5]`.  
Collectiosn by default are **only** allowed as the last arguement, for example:
```java
void execute(Sender sender, int number, List<String> args);
```
With one exception being a split argument.

### Split argument
A split argument is a collection that is annotated by `@Split`, example:  
Given the command `/foo bar diamond,iron_ingot,stone,grass_block 5`, can be declared as:  
```java
void execute(Sender sender, @Split(",") List<Material> materials, int amount) {
    println(materials); // Would print [DIAMOND, IRON_INGOT, STONE, GRASS_BLOCK]
}
```

### Join argument
The same way you can split a string into a collection, you can also join a list of arguments into a single string.  
This however can only be used as the last argument of the command.  
Command example: `/foo bar 5 hello there people`.
```java
void excecute(Sender sender, int number, @Join(", ") String message) {
    println(message); // Would print "hello, there, people"
}
```

## Flags
I've decided to dedicate an entire page explaining Flags instead, which you can find [here](/).


