<center><h1>Using States</h1></center>
<center><p>Quick example on how to use States.</p></center>

---

!!!v  
All examples are for the Paper platform, but it should be similar if not identical in other platforms.  
!!!

!!!!  
Kotlin examples require the `dev.triumphteam:triumph-gui-<platform>kotlin:<version>` dependency.
!!!

# Title and states

States can also be applied to titles, which means we can share them between a component and a title making a component
update the title.

For this example, let's add a "highScore" in the title, where within the current game session we keep track of the
highest number of clicks you did.  
For that we need to create a state that is not in the same place as the opening of the GUI. For example as a field in a
command class.

For this state it's nice to make it so it can only be updated if the clicks are higher than the stored value. Thankfully
we can use a (StateMutationPolicy)[/mutation-policy] for that, so let's create a new one!

-+-  
+Java+

```java
public final class HighScoreMutationPolicy implements StateMutationPolicy<Integer> {

    @Override
    public boolean shouldMutate(@Nullable final Integer currentValue, @Nullable final Integer newValue) {
        if (currentValue == null || newValue == null) return false;
        // Only allow mutation if the new value is higher
        return newValue > currentValue;
    }
}
```

+++  
+Kotlin+

```kotlin
class HighScoreMutationPolicy : StateMutationPolicy<Int?> {

    override fun shouldMutate(currentValue: Int?, newValue: Int?): Boolean {
        if (currentValue == null || newValue == null) return false
        // Only allow mutation if the new value is higher
        return newValue > currentValue
    }
}
```

+++  
-+-

_The mutation policy in this example is not really needed; this is just an example of how it can be used._

Now let's create a state with the new policy.

-+-  
+Java+

```java
private final MutableState<Integer> highScoreState = MutableState.of(0, new HighScoreMutationPolicy());
```

+++  
+Kotlin+

```kotlin
private val highScoreState = mutableStateOf(0, HighScoreMutationPolicy())
```

+++  
-+-

Then we can change the GUI to support it.

-+-  
+Java+

```java
final var gui = Gui.of(1)
        .spamPreventionDuration(0) // Changing the spam prevension to allow faster clicking, for fun
        .title(title -> {
            // Tell the title to remember the high score state
            title.remember(highScoreState);
            // Then render the title with the high score value
            title.render(() -> Component.text("Cookie clicker! Highest score: " + highScoreState.get()));
        })
        .component(component -> {

            // We tell the component to remember the starting value `0`
            // Which will return a MutableState<Integer> that can be used in the render function of the component
            final var clicks = component.remember(0);

            // Here is where the component will be rendered
            component.render(container -> {

                // Like before, we set the item in the middle of the inventory
                // Let's also change the item to a COOKIE
                container.setItem(1, 5, ItemBuilder.from(Material.COOKIE)
                        // We append the value of the clicks state to the name of the item
                        .name(Component.text("Clicked " + clicks.get() + " times!"))
                        .asGuiItem((player, context) -> {
                            // Now we update the clicks state by adding 1 to the previous amount
                            clicks.update(previous -> previous + 1);

                            // Set the value to the high score state
                            // Because of the policy we added, it means that this will only actually change the state
                            // if the value is higher than the current value
                            highScoreState.set(clicks.get());

                            // As stated before, the mutation policy isn't really needed, could have just been
                            // something like if (clicks.get() > highScore.get()) highScore.set(clicks.get())
                            // both are totally fine
                        })
                );
            });
        })
        .build();

gui.open(player);
```

+++  
+Kotlin+

```kotlin
val gui = buildGui {
    // If not set, defaults to chest - 1 row
    // So in this case this wouldn't be needed, leaving it here as an example
    containerType = chestContainer {
        rows = 1
    }

    // Delegate the value of the state
    // Not needed, but it's nicer to work with
    var highScore by highScoreState

    title {
        // Tell the title to remember the high score state
        remember(highScoreState)
        // Then render the title with the high score value
        render { Component.text("Cookie clicker! Highest score: $highScore") }
    }

    // We use stateless since we don't need any updates for this example
    component {

        // We tell the component to remember the starting value `0`
        // Which will return a MutableState<Integer> that can be used in the render function of the component
        var clicks by remember(0)

        // Here is where the component will be rendered
        render { container ->

            // Like before, we set the item in the middle of the inventory
            // Let's also change the item to a COOKIE
            container[1, 5] = ItemBuilder.from(Material.DIAMOND)
                .name(Component.text("Clicked $clicks times!"))
                .asGuiItem { _, _ ->
                    // Now we increase the clicks state by 1
                    clicks++

                    // Set the value to the high score state
                    // Because of the policy we added, it means that this will only actually change the state
                    // if the value is higher than the current value
                    highScore = clicks

                    // As stated before, the mutation policy isn't really needed, could have just been
                    // something like if (clicks > highScore) highScore = clicks
                    // both are totally fine
                }
        }
    }
}

gui.open(player)
```

+++  
-+-

When the GUI is opened for the first time the title will update with the clicks, once you close and re-open it, it'll
only update once you reach a new high score.

# Finalizing

Now that you have seen the examples and learned how to build a GUI, continue reading on the more in-depth aspects of the 
library.
