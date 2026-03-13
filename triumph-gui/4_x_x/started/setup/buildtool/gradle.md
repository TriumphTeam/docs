{gradle-example}
_Make sure to replace `[version]` with the latest version._  
To include the lib in your project, you need to add the `shadow` plugin.  
Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.

```kotlin
plugins {
    // Make sure to keep the shadow plugin up to date.
    id("com.gradleup.shadow") version "9.2.2"
}

shadowJar {
   relocate("dev.triumphteam.gui", "[YOUR PACKAGE].gui")
   relocate("dev.triumphteam.nova", "[YOUR PACKAGE].nova") // States library.
}
```
When using the shadow plugin, make sure to use the `shadowJar` task and to select the correct jar file once the project is built.
