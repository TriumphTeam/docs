You need to add the dependency to your `build.gradle.kts`.

```kotlin
repositories {
    mavenCentral()
}

dependencies {
    implementation("dev.triumphteam:triumph-gui:[version]")
}
```
_Make sure to replace `[version]` with the latest version._  
To include the lib in your project, you need to add `shadowJar` plugin `build.gradle.kts`.  
Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.

```kotlin
plugins { 
    id("com.gradleup.shadow") version "9.2.2"
}

shadowJar {
   relocate("dev.triumphteam.gui", "[YOUR PACKAGE].gui")
}
```
