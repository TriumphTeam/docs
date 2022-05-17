<center><h1>Command Manager</h1></center>
<center>
<p>The basic entry for everything related to your commands.</p>
</center>

---

# Creating a command manager
Each platform has it's own command manager and each manager has it's own sender type.
```java
// Bukkit
BukkitCommandManager<CommandSender> manager = BukkitCommandManager.create(plugin);

// JDA Prefixed
PrefixedCommandManager<PrefixedSender> manager = PrefixedCommandManager.create(jda);

// JDA slash
SlashCommandManager<SlashSender> manager = SlashCommandManager.create(jda);
```
The type parameter for the sender is necessary because you can also specify your own sender type by passing a custom `SenderMapper`. You can read more about it [here](/library/triumph-cmds/custom-senders).  

# Usage
The command manager is used for doing everything for the commands, registering commands, messages, arguments, etc.