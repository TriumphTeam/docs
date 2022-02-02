<center><h1>Setup</h1></center>
<center>
<p>This is how you add the lib to your project.</p>
</center>

---

# Version
Make sure to replace `{version}` with the latest versions (`%version%`).

# Platform
Make sure to replace `{platform}` with one of the following:

* `bukkit` - For any Bukkit based plugin, Spigot, Paper, etc.
* `jda-prefixed` - For prefixed commands for JDA, for example `!test`.
* `jda-slash` - For JDA slash commands.

-+-
+Gradle (Kotlin)+
You need to add the dependency to your `build.gradle.kts`.
```kotlin
repositories {
    maven("https://repo.triumphteam.dev/snapshots/")
}

dependencies {
    implementation("dev.triumphteam:triumph-cmds-{platform}:{version}") // Replace version here 
}
```
In order to include the lib in your project, you need to add `shadow` plugin `build.gradle.kts`.  
Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.
```kotlin
// This goes on the top of the build script.
plugins {
    id("com.github.johnrengelman.shadow") version "7.0.0"
}

// This can go anywhere.
shadowJar {
   relocate("dev.triumphteam.cmd", "[YOUR PACKAGE].cmd")
}
```
+++
+Gradle (Groovy)+
You need to add the dependency to your `build.gradle`.
```groovy
repositories {
    maven { url = "https://repo.triumphteam.dev/snapshots/" }
}

dependencies {
    implementation "dev.triumphteam:triumph-cmds-{platform}:{version}" // Replace version here 
}
```
In order to include the lib in your project, you need to add `shadow` plugin `build.gradle`.  
Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.
```groovy
// This goes on the top of the build script.
plugins {
    id "com.github.johnrengelman.shadow" version "7.0.0"
}

// This can go anywhere.
shadowJar {
   relocate("dev.triumphteam.cmd", "[YOUR PACKAGE].cmd")
}
```
+++
+Maven+
You need to add the dependency to your `pom.xml`.
```xml
<repositories>
    <repository>
        <id>repo</id>
        <url>https://repo.triumphteam.dev/snapshots/</url>
    </repository>
</repositories>

<dependency>
    <groupId>dev.triumphteam</groupId>
    <artifactId>triumph-cmd-{platfomr}</artifactId>
    <version>{version}</version> <!-- replace version here -->
</dependency>
```
In order to include the framework in your project, you need the shade plugin.  
Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-shade-plugin</artifactId>
    <version>3.1.1</version>
    <configuration>
        <relocations>
            <relocation>
                <pattern>dev.triumphteam.cmd</pattern>
                <shadedPattern>[YOUR PACKAGE].cmd</shadedPattern> <!-- Replace package here here -->
            </relocation>
        </relocations>
    </configuration>
    <executions>
        <execution>
            <phase>package</phase>
            <goals>
                <goal>shade</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```
+++
-+-
