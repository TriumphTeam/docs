```java
.title(title -> {
    // Tell the title to remember the high-score state.
    title.remember(highScoreState);
    // Then render the title with the high score value.
    title.render(() -> Component.text("Cookie clicker! Highest score: " + highScoreState.get()));
})
```
