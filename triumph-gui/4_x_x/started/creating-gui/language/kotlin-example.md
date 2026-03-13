```kotlin
val gui = buildGui {
    containerType = chestContainer(rows = 1)
    title(Component.text("My Simple GUI!"))
    // We use stateless since we don't need any updates for this example.
    statelessComponent { container ->
        container[1, 5] = ItemBuilder.from(Material.DIAMOND)
            .name(Component.text("Click me!"))
            .asGuiItem { player, context ->
                player.sendMessage("You have clicked the item!")
            }
    }
}

// Now that the GUI is built, we can open it for the player.
gui.open(player)
```
