<center><h1>Using States</h1></center>
<center><p>Quick example on how to use States.</p></center>

---

!!!v  
All examples are for the Paper platform, but it should be similar if not identical in other platforms.  
!!!

!!!!  
Kotlin examples require the `dev.triumphteam:triumph-gui-<platform>kotlin:<version>` dependency.
!!!

# Adding state

A quick explanation of a [State](/states) is that it's an object that can be "tied" to a [Component](/components) which when 
modifier cause the component to re-render.  

Let's take the previous example and add some a state to it. We can create a state that'll keep track of how many times 
a `player` has clicked on the item.  

-+-  
+Java+  

```java
final var gui = Gui.of(1)
        .title(Component.text("Cookie clicker!"))
        .component(component -> { // This time we want a normal component

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

    title(Component.text("Cookie clicker!"))

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
                }
        }
    }
}

gui.open(player)
```
+++  
-+-  
Congratulations you have built the most simple cookie clicker game!  
But we can improve it even more, let's add title updating into the mix, read more in [here](/updating-title).
