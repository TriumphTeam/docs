<center><h1>Setup</h1></center>
<center><p>Adding the library to your project.</p></center>

---

-+-
+Gradle (Kotlin)+
You need to add the dependency to your `build.gradle.kts`.

```kotlin
repositories {
    maven("https://repo.triumphteam.dev/snapshots")
}

dependencies {
    implementation("dev.triumphteam:triumph-gui-paper:4.0.0-SNAPSHOT")
}
```

 To include the lib in your project, you need to add `shadowJar` plugin `build.gradle.kts`.  
 Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.

```kotlin
plugins { 
    id("com.gradleup.shadow") version "8.3.3"
}

shadowJar {
   relocate("dev.triumphteam.gui", "[YOUR PACKAGE].gui")
}
```
+++
+Gradle (Groovy)+
You need to add the dependency to your `build.gradle`.

```groovy
repositories {
    maven {
        url = uri("https://repo.triumphteam.dev/snapshots")
    }
}

dependencies {
    implementation "dev.triumphteam:triumph-gui-paper:4.0.0-SNAPSHOT"
}
```

 To include the lib in your project, you need to add `shadowJar` plugin `build.gradle`.  
 Replace `[YOUR PACKAGE]`with your plugin's package, for example `me.myplugin.plugin`.

```groovy
plugins {
    id "com.gradleup.shadow" version "8.3.3"
}

shadowJar {
   relocate("dev.triumphteam.gui", "[YOUR PACKAGE].gui")
}
```
+++

+Maven+
You need to add the dependency to your pom.xml.

```xml
<repositories>
    <repository>
        <id>repo</id>
        <name>TriumphTeam</name>
        <url>https://repo.triumphteam.dev/snapshots</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>dev.triumphteam</groupId>
        <artifactId>triumph-gui-paper</artifactId>
        <version>4.0.0-SNAPSHOT</version>
    </dependency>
</dependencies>
```

 To include the library in your project, you need to add the following to your `pom.xml`, in the plugins section.  
 Replace `[YOUR PACKAGE]`with your plugin's package, for example `me.myplugin.plugin`.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-shade-plugin</artifactId>
    <version>3.6.0</version>
    <configuration>
        <relocations>
            <relocation>
                <pattern>dev.triumphteam.gui</pattern>
                <shadedPattern>[YOUR PACKAGE].gui</shadedPattern> <!-- Replace package here here -->
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
