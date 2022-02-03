<center><h1>GUI Features</h1></center>
<center>
<p>After the basics of a GUI there is a lot more useful features you can use.</p>
</center>

## Common features

The following are the common features in all GUIs.

# Filler

The GUI filler allows you to fill in the GUI in many ways, for example, completely filling or filling the bottom or top of the GUI. You can get the filler by doing `GUI#getFiller`.

Setting you fill item will fill the slots in your GUI that doesn't contain a GUI item.

```java
// Single fill item
gui.getFiller().fill(ItemBuilder.from(Material.BLACK_STAINED_GLASS_PANE)).asGuiItem());

// Multiple fill items
gui.getFiller().fill(Arrays.asList(ItemBuilder.from(Material.BLACK_STAINED_GLASS_PANE)).asGuiItem(), ItemBuilder.from(Material.WHITE_STAINED_GLASS_PANE)).asGuiItem()));
```

Just like any other item these items can also have a click action, but they'll be the same for all the slots it is filled.

# Set default click action

You can also set a default click action, which will be applied to every single slot in the GUI. For example if you call `event.setCancelled(true)` as your default action, you no longer need to cancel it for every single item.

```java
gui.setDefaultClickAction(event -> {
    // Handle your default action here
});
```

# Set close GUI action

This will display the action you set when ever the GUI is closed.  
The event passed down for this action is the `InventoryCloseEvent`.

```java
gui.setCloseGuiAction(event -> {
    // Handle your close action
});
```

# Set open GUI action

This will display the action you set when ever the GUI is open .  
The event passed down for this action is the `InventoryOpenEvent`.

```java
gui.setOpenGuiAction(event -> {
    // Handle your open action
});
```

# Slot actions

If you want to add a click action to a specif slot without needing to have to specify the item in the slot, you can simple use the `setSlotAction`.  
It also supports both rows and columns and slots.

```java
// With slot
gui.addSlotAction(slot, event -> {
    // Handle your open action
});

// With rows and collumns
gui.addSlotAction(row, col, event -> {
    // Handle your open action
});
```

# Update

The `update` method will update the entire GUI except the title, due to how inventories work.

```java
gui.update();
```

# Update title

This will also update the title but you need to pass the new title down. _This feature has not been tested enough_.

```java
gui.updateTitle(Component.text("New Title"));
```

# Update Item

This is the preferable way of making updates in your GUI, for example an item that keeps refreshing, etc.  
This is recommended over the other ones as it'll simply change one item instead of the whole GUI.  
It also supports both rows and columns and slots.

```java
// Using slots
gui.updateItem(slot, new ItemStack(Material.STONE));

// Using rows and collumns
gui.updateItem(row, col, new ItemStack(Material.STONE));
```

# Item Builder

Triumph-GUI already comes with a built in `ItemBuilder` to make it easier for you to create custom items.
