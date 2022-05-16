<center><h1>Messages</h1></center>
<center>
<p>Customization of error/invalid usage messages.</p>
</center>

---

# Messages
The library provides many messages that are configurable through a simple structure. Any message that you modify
will be handled using the function and syntax displayed below in the example provided.

```java
commandManager.registerMessage(MessageKey.INVALID_ARGUMENT, (sender, context) -> {
    // handle sending the error message
});
```

Different use-cases provide different applicable keys. You can find a list of all available keys for each module below.

## Universal Keys
Universal keys are accessed through the `MessageKey` class.
* `INVALID_ARGUMENT`
* `TOO_MANY_ARGUMENTS`
* `NOT_ENOUGH_ARGUMENTS`
* `UNKNOWN_COMMAND`

## Bukkit Keys
Bukkit keys are accessed through the `BukkitMessageKey` class.
* `NO_PERMISSION`
* `PLAYER_ONLY`
* `CONSOLE_ONLY`

