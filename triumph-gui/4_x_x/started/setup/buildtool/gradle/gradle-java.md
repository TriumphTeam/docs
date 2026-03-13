```kotlin
repositories {
    mavenCentral()
}

dependencies {
    implementation("dev.triumphteam:triumph-gui-paper:[version]")
}

java {
    toolchain.languageVersion.set(JavaLanguageVersion.of(21))
}
```
