<center><h1>Arguments</h1></center>
<center><p>Command argument declaration and options.</p></center>

---

# Named Arguments
Named arguments allow for arguments to be named. So instead of a command being `/foo bar baz 1`, this will allow for `/foo bar string:baz, number:1`.
This also allows for arguments to be inputted in any order!

## Example of Named Arguments
Firstly, we must register the named arguments
CommandManager#registerNamedArguments either takes a varag of `Argument`s or a `List<Argument>`.
```java
commandManager.registerNamedArguments(ArgumentKey.of("example"), // the key of the argument
    Argument.forString().name("string").build(), // a description and suggestion can also be set in the argument builder!
    Argument.forInt().name("number").build());
```

Now we need to setup our command:
```java
@NamedArguments("example")
void execute(Sender sender, Arguments arguments) {
    println("string=" + arguments.get("string", String.class).get() + ", number=" + arguments.get("number", int.class).get()); // outputs string=baz, number=1
    // this is just an example, please dont use Optional#get without checking if the value is present/empty first!
}
```
