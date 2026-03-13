```java
// Once again we start the state at 0.
final var highScoreState = MutableState.of(0);

final var gui = Gui.of(1)
        // Using a functional title instead of just a static one like before.
        .title(title -> {
            // Tell the title to remember the high-score state.
            title.remember(highScoreState);
            // Then render the title with the high score value.
            title.render(() -> Component.text("Cookie clicker! Highest score: " + highScoreState.get()));
        })
        .component(component -> {
            // We tell the component to remember a state with a starting value of `0`.
            // Which will return a MutableState<Integer> that can be used in the render function of the component.
            final var clicks = component.remember(0);

            // Here is where the component will be rendered.
            component.render(container -> {
                // We add the cookie item.
                container.setItem(1, 5, ItemBuilder.from(Material.COOKIE)
                        .name(Component.text("Clicked " + clicks.get() + " times!"))
                        .asGuiItem((player, context) -> {
                            // Now we update the "clicks" state by adding 1 to the previous amount.
                            clicks.update(previous -> previous + 1);
                            // And also, we update the highscore!
                            highScoreState.update(highest -> Math.max(highest, clicks.get()));
                        })
                );

                // And a button to reset the game.
                container.setItem(1, 9, ItemBuilder.from(Material.BARRIER)
                        .name(Component.text("Restart game"))
                        .asGuiItem((player, context) -> {
                            // Just reset the clicks to 0.
                            clicks.set(0);
                        })
                );
            });
        })
        .build();

// Now that the GUI is built, we can open it for the player.
gui.open(player);
```
