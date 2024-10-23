<center><h1>Creating a GUI</h1></center>
<center><p>Create, setup, and open.</p></center>

---

!!!v  
All examples are for the Paper platform, but it should be similar if not identical in other platforms.  
!!!

!!!!  
Kotlin examples require the `dev.triumphteam:triumph-gui-<platform>-kotlin:<version>` dependency.
!!!

# Starting

To create a [GUI](/gui), we call the builder for the desired [Container Type](/container-type). This will return a GUI
builder.  
The builder allows you to setup all the components as well as personalize how the GUI should function. Like for example
setting custom [renderer](/renderer)s.

Let's create a GUI with a `1` row and an item the middle that sends the `player` a message when clicking.

-+-
+Java+

```java
final var gui = Gui.of(1)
        .title(Component.text("My Simple GUI!"))
        .statelessComponent(container -> { // We use stateless since we don't need any updates for this example
            container.setItem(1, 5, ItemBuilder.from(Material.DIAMOND)
                    .name(Component.text("Click me!"))
                    .asGuiItem((player, context) -> {
                        player.sendMessage("You have clicked on the diamond item!");
                    })
            );
        })
        .build();

// Now that the GUI is built, we can open it for the player.
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

    title(Component.text("My Simple GUI!"))

    // We use stateless since we don't need any updates for this example
    statelessComponent { container ->
        container[1, 5] = ItemBuilder.from(Material.DIAMOND)
            .name(Component.text("Click me!"))
            .asGuiItem { player, _ ->
                player.sendMessage("You have clicked on the diamond item!")
            }
    }
}

// Now that the GUI is built, we can open it for the player.
gui.open(player)
```
+++
-+-

Now that the GUI is created, we can dive into something more complex by utilizing [States](/states).  
We can continue onto the next example [here](/using-states).
