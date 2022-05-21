<center><h1>Core</h1></center>
<center>
<p>Basics about the core.</p>
</center>

---

# Core
This library is heavily based on the Kotlin framework **[ktor](https://ktor.io/)**.  
The main utility of the core library is to simplify adding and getting "features" of the plugin.  

# What are features?
"Feature" is a concept for anything that adds to the application. You can think of it like "register-ables", something that you can register and use later.
For example, you want a "PlayerManager", you can turn that into a "feature" that can be easily installed with `install(PlayerManager)` and gotten with `feature(PlayerManager)`.  

# Platforms
Currently, you can use it for `Bukkit` and `JDA`.

# Creating a feature
Firstly let's create a simple feature that allows us to print `hello`.
```kotlin
// Main feature class
class Print {

    // Function we want to call from the feature
    fun printHello() {
        println("hello")
    }

    // Feature companion, the type parameters are <ApplicationType, FeatureConfiguration, Feature>
    // The configuration can be anything, therefore also the main feature
    companion object Feature : ApplicationFeature<TriumphApplication, Print, Print> {
        override val key = key<Print>("print")

        override fun install(application: TriumphApplication, configure: Print.() -> Unit): Print {
            // Creates an instance of the feature and applies the configuration
            return Print().apply(configure)
        }
    }
}
```

# Creating a Bukkit application
As an example let's create a simple application (plugin) to use our feature.
```kotlin
class MyPlugin : BukkitApplication() {

    override fun onEnable() {
        // Installing our first feature
        install(Print)
    }
}
```
Now let's say we want to use the `printHello` function.
```kotlin
// If you are not sure if the application is present you can use `featureOrNull` instead
// Or alternatively you can also do application[Print]
val print = application.feature(Print)
print.printHello()
```
