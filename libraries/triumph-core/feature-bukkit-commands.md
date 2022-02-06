<center><h1>Bukkit commands feature</h1></center>
<center>
<p>Feature that simplifies using and registering commands.</p>
</center>

---

# Creating the commands feature
For now let's just use the default `CommandSender` for bukkit, but this feature allows you to use custom ones.  
This is useful because you can completely abstract the code to work on multiple platforms without much change if any at all.
```kotlin
class MyCommands(plugin: BukkitApplication) :
    Commands<CommandSender>(plugin, SenderMapper.defaultMapper(), Validator()) {

    companion object Feature : CommandFeature<CommandSender, BukkitApplication, MyCommands, MyCommands> {

        override val key = key<MyCommands>("my-commands")

        override fun install(application: BukkitApplication, configure: MyCommands.() -> Unit): MyCommands {
            return MyCommands(application).apply(configure)
        }
    }
}
```

# Registering commands
Now that the feature is created, you can either install it with `install(MyCommands)` or just use the `commands` block directly.  
```kotlin
override fun onEnable() {
    commands(MyCommands) {
        // Registering a suggestion
        suggestion(SuggestionKey.of("example")) { listOf("example1", "example2", "example3")}

        // Registering an argument
        argument<Material> { sender, arg -> Material.matchMaterial(arg) }

        // Registering commands
        register(
            CommandOne(),
            CommandTwo(),
            CommandTree(),
        )
    }
}