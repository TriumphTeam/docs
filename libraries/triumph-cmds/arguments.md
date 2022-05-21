<center><h1>Arguments</h1></center>
<center>
<p>Command argument declaration and options.</p>
</center>

---

# Concept
The concept of arguments in the library are based on parameters, each parameter declared in the method will be a command argument.

# Sender
The first parameter of the command method **must** always be a sender. You can read more about the sender [here](/).

# Creating a command with arguments
Let's create the following command `/give item diamond 5`. Where `give` is the command, `item` is the sub command, `diamond` is an argument of type `Material` and `5` is the amount or an `int`.
```java
@Command("give")
class MyClass extends BaseCommand {

    @SubCommand("item")
    public void execute(Sender sender, Material material, int amount) {
        sender.sendMessage("The selected material was: " + material); // Will send "DIAMOND"
        sender.sendMessage("The amount was: " + amount); // Will send "5"
    }
}
```
It is as simple as that to have arguments for your command.

## Argument Names
By default, argument names will be defined as the name of the parameter.

The `@ArgName` annotation is used to define the name of the argument should you not want the name of the argument
to be the same as the name of the parameter. If you would like to use the parameter name as the 
argument name, you can use the `-parameters` compiler flag when compiling your plugin.
```java
@SubCommand("id")
public void execute(Sender sender, @ArgName("username") Player target) {
    sender.sendMessage(target.getName() + " has the id: " + target.getUniqueId());
}
```
In this case, the argument will be called `username` instead of the parameter name, `target`.