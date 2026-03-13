{maven-example}
_Make sure to replace `[version]` with the latest version._  
To include the library in your project, you need to add the `shade` plugin to your `pom.xml`, in the plugins section.  
Replace `[YOUR PACKAGE]` with your plugin's package, for example `me.myplugin.plugin`.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-shade-plugin</artifactId>
    <version>3.6.1</version> <!-- Keep this version up to date! -->
    <configuration>
        <relocations>
            <relocation>
                <pattern>dev.triumphteam.gui</pattern>
                <!-- Replace the package here. -->
                <shadedPattern>[YOUR PACKAGE].gui</shadedPattern> 
            </relocation>
            <relocation>
                <pattern>dev.triumphteam.nova</pattern>
                <!-- Replace the package here too, this is the 'states' library. -->
                <shadedPattern>[YOUR PACKAGE].nova</shadedPattern>
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
To shade the library into your jar, make sure to use the `package` task and to select the correct jar file once the project is built.
