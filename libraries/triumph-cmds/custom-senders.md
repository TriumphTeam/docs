<center><h1>Custom Senders</h1></center>
<center>
<p>Custom senders creation and registration.</p>
</center>

---

# Creating a simple sender
```java
public class MySender {}
```

# Creating a SenderValidator
Sender Validators are used for pre command checks.
```java
public class MySenderValidator implements SenderValidator<MySender> {

    // This method is used when registering, it'll check if the sender declared in the command method is valid or not
    @Override
    public @NotNull Set<Class<? extends MySender>> getAllowedSenders() {
        return Collections.singleton(MySender.class);
    }

    @Override
    public boolean validate(final @NotNull MessageRegistry<MySender> messageRegistry, final @NotNull SubCommand<MySender> subCommand, final @NotNull MySender sender) {
        // Do any checks you want here, for example on Bukkit, this is where it checks if the subcommand is console only, or player only, etc
        // Return true if valid, false, if not, use the message registry to send messages to the player if you want
        return false;
    }
}
```
Now you can either make a custom SenderMapper or just use lambda.
If you're not using lambda, then make sure you speccify the correct senders. If you're using lambda it will be a little bit easier.
```java
class MyMapper implements SenderMapper<CommandSender, MySender>
```
Now time to create the command manager. We will be using the BukkitCommandManager for this example.
```java
final BukkitCommandManager<MySender> manager = BukkitCommandManager.create(
        plugin,
        defaultSender -> new MySender(), // The mapping of the sender, pass a new instance if you don't want lambda
        new MySenderValidator() // Validator
);
```
That is all! You can now register a new command with your custom sender.
```java
@Command("foo")
class MyCommand extends BaseCommand {

	@Default
	public void executor(MySender sender) {
		// Code to be executed
	}
}
```
You can learn how to create and register commands [here](/library/triumph-cmds/commands).