<center><h1>Arguments</h1></center>
<center>
<p>Command argument declaration and options.</p>
</center>

---

# Registering arguments
If you wish to create your own arguments, you can do so by using `CommandManager#registerArgument`.
This method takes 2 parameters, the first being a `Class`. This class is what will be used when defining the parameters of the command.
The second parameter is a lambda with 2 parameters, the first being the Sender object and the second being a String representing the argument input.

## Example of registering arguments
```java
commandManager.registerArgument(LocalDate.class, (sender, argument) -> LocalDate.parse(argument));
```

Now we need to use this argument in our command, given the command `/foo bar 2000-01-01`:
```java
void execute(Sender sender, LocalDate date) {
    println(date); // outputs 2000-01-01
}
```
