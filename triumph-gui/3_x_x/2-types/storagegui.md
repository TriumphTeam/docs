<center><h1>StorageGUI</h1></center>
<center><p>GUI that does not clear its items on close/open, any external non GuiItem added to it will stay.</p></center>

!!!!  
Attention! Items stored inside this GUI will not Persist on Server Restart.  
!!!

# Storage GUI

![](https://i.imgur.com/fcqrvnp.gif)

# Creating a Persistent GUI

To create a persistent GUI all you need to do is:

```java
StorageGui gui = Gui.storage()
        .title(Component.text("GUI Title!"))
        .rows(6)
        .create();
```

Just like the normal [GUI](/gui) the first parameter is the rows the GUI should have.

# Adding the item to the GUI

Differently to the normal [GUI](/gui), the `addItem` method takes an `ItemStack` instead. Any `GuiItem` added will have actions applied to it;
the persistent items are simple ItemStacks that have nothing associated to it.
