<center><h1>Commands</h1></center>
<center><p>The basic structure of a command, and its sub commands.</p></center>

---

# Creating a simple command
Every command must extend `BaseCommand`.  
You can use the `@Command` annotation to declare the command name and alias.
```java
@Command("foo")
class MyCommand extends BaseCommand {}
```
A command can also have aliases.
```java
@Command(value = "foo", alias = {"bar", "baz"})
class MyCommand extends BaseCommand {}
```
Alternatively you can also declare the command name and alias through the `BaseCommand`'s constructor.
```java
class MyCommand extends BaseCommand {
    
    public MyCommand() {
        super("foo", Arrays.asList("bar", "baz"));
    }
}
```
!!!!
The usage of the keyword `Sender` in the following examples are **not** the correct name, it just represents a sender.  
As the real sender name can change based on platform or the provided custom sender.
!!!

# Sub commands
Each sub commands are declared by methods, currently there is no other way to declare its name and alias other than through annotations.

## Default
A `@Default` method is a "sub command without a name", implying it is the main executor of a command that has no sub commands.  
For example the command `/foo` would be declared in the following way:
```java
@Command("foo")
class MyCommand extends BaseCommand {

    @Default
    public void executor(Sender sender) {
        // Code to be executed
    }
}
```

## SubCommand
A `@SubCommand` is a sub command that has a specific name. For example `/foo bar`
```java
@Command("foo")
class MyCommand extends BaseCommand {

    @SubCommand("bar")
    public void executor(Sender sender) {
        // Code to be executed
    }
}
```

## Alias
Both annotations also support an alias to be passed:  
`@Default(alias = {"bar"})` would be executed as either `/foo` or `/foo bar`.  
`@SubCommand(value = "bar", alias = {"baz"})` would be executed as either `/foo bar` or `/foo baz`.

# Registering
Registering the command is very simple, you simply do:
```java
commandManager.registerCommand(new MyCommand());
```
