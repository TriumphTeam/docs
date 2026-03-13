```kotlin
val gui = buildGui {
    containerType = chestContainer(rows = 1)
    title(Component.text("Cookie clicker!"))
    // This time we want a normal component.
    component {
        // We tell the component to remember a state with a starting value of `0`.
        // Which delegates a MutableState<Int> and returns an Int that can be used in the render function of the component.
        var clicks by remember(0)

        // Here is where the component will be rendered.
        render { container ->
            // Like before, we set the item in the middle of the inventory.
            // Let's also change the item to a cookie!
            container[1, 5] = ItemBuilder.from(Material.COOKIE)
                // We append the value of the "clicks" state to the name of the item.
                .name(Component.text("Clicked $clicks times!"))
                .asGuiItem { player, context ->
                    // Now we update the "clicks" state by incrementing it by 1.
                    clicks++
                }
        }
    }
}

// Now that the GUI is built, we can open it for the player.
gui.open(player)
```
