You need to add the dependency to your `pom.xml`.

```xml
<dependency>
    <groupId>dev.triumphteam</groupId>
    <artifactId>triumph-gui</artifactId>
    <version>[version]</version>
</dependency>
```
_Make sure to replace `[version]` with the latest version._  
To include the framework in your project, you need to add the following to your `pom.xml`, in the plugins section.  
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
