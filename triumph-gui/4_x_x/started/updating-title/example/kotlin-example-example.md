```kotlin
val gui = buildGui {
    containerType = chestContainer(rows = 1)
    
    // Once again we start the state at 0.
    // We also don't use "by" here, we don't want to delegate the value just yet.
    // We need the MutableState instance so we can tell the title to remember it.
    val highScoreState = mutableStateOf(0)
    
    // Using a functional title instead of just a static one like before.
    title {
        // Tell the title to remember the high-score state and delegate the value to a variable we can use.
        val highScore by remember(highScoreState)
        // Then render the title with the high score value.
        render { Component.text("Cookie clicker! Highest score: $highScore") }
    }
    component {
        // We tell the component to remember a state with a starting value of `0`.
        // Which will return a MutableState<Integer> that can be used in the render function of the component.
        var clicks by remember(0)
        // We delegate the high-score state to a variable here.
        // We don't need to "remember" it because the click
        // component doesn't need to update when the high-score changes.
        var highScore by highScoreState

        // Here is where the component will be rendered.
        render { container ->
            // We add the cookie item.
            container[1, 5] = ItemBuilder.from(Material.COOKIE)
                .name(Component.text("Clicked $clicks times!"))
                .asGuiItem { player, context ->
                    // Now we update the "clicks" state by adding 1 to the previous amount.
                    clicks++
                    // And also, we update the highscore!
                    highScore = max(highScore, clicks)
                }

            // And a button to reset the game.
            container[1, 9] = ItemBuilder.from(Material.BARRIER)
                .name(Component.text("Restart game"))
                .asGuiItem { player, context ->
                    clicks = 0
                }
        }
    }
}

// Now that the GUI is built, we can open it for the player.
gui.open(player)
```
