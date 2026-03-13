```kotlin
title {
    // Tell the title to remember the high-score state and delegate the value to a variable we can use.
    val highScore by remember(highScoreState)
    // Then render the title with the high score value.
    render { Component.text("Cookie clicker! Highest score: $highScore") }
}
```
