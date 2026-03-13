```java
final var gui = Gui.of(1)
        .title(Component.text("Cookie clicker!"))
        // This time we want a normal component.
        .component(component -> {
            // We tell the component to remember a state with a starting value of `0`.
            // Which will return a MutableState<Integer> that can be used in the render function of the component.
            final var clicks = component.remember(0);

            // Here is where the component will be rendered.
            component.render(container -> {
                // Like before, we set the item in the middle of the inventory.
                // Let's also change the item to a cookie!
                container.setItem(1, 5, ItemBuilder.from(Material.COOKIE)
                        // We append the value of the "clicks" state to the name of the item.
                        .name(Component.text("Clicked " + clicks.get() + " times!"))
                        .asGuiItem((player, context) -> {
                            // Now we update the "clicks" state by adding 1 to the previous amount.
                            clicks.update(previous -> previous + 1);
                            // You can also use `clicks.set(clicks.get() + 1);`.
                        })
                );
            });
        })
        .build();

// Now that the GUI is built, we can open it for the player.
gui.open(player);
```
