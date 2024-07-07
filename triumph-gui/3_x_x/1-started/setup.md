<center><h1>Setup</h1></center>
<center><p>Adding the library to your project.</p></center>

---

-+-  
+Gradle (Kotlin)+
You need to add the dependency to your `build.gradle.kts`.

```kotlin
repositories {
    mavenCentral()
}

dependencies {
    implementation("dev.triumphteam:triumph-gui:%version%")
}
```

 In order to include the lib in your project, you need to add `shadowJar` plugin `build.gradle.kts`.  
 Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.

```kotlin
plugins {
    id("com.github.johnrengelman.shadow") version "7.1.1"
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
    mavenCentral()
}

dependencies {
    implementation "dev.triumphteam:triumph-gui:%version%"
}
```

 In order to include the lib in your project, you need to add `shadowJar` plugin `build.gradle`.  
 Replace `[YOUR PACKAGE]`with your plugin's package, for example `me.myplugin.plugin`.

```groovy
plugins {
    id "com.github.johnrengelman.shadow" version "7.1.1"
}

shadowJar {
   relocate("dev.triumphteam.gui", "[YOUR PACKAGE].gui")
}
```
+++

+Maven+
You need to add the dependency to your pom.xml.

```xml
<dependency>
    <groupId>dev.triumphteam</groupId>
    <artifactId>triumph-gui</artifactId>
    <version>%version%</version>
</dependency>
```

 In order to include the framework in your project, you need to add the following to your `pom.xml`, in the plugins section.  
 Replace `[YOUR PACKAGE]`with your plugin's package, for example `me.myplugin.plugin`.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-shade-plugin</artifactId>
    <version>3.2.4</version>
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
