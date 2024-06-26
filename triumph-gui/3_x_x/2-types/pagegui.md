<center><h1>PaginatedGUI</h1></center>
<center>
<p>Simple GUI that allows you to have multiple pages and navigate between them.</p>
</center>

# Paginated GUI

![](https://i.imgur.com/PqNYUIs.gif)

# Creating a Paginated GUI

To create a Paginated GUI all you need to do is:

```java
// Main constructor
PaginatedGui gui = Gui.paginated()
        .title(Component.text("GUI Title!"))
        .rows(6)
        .pageSize(45) // Set the size you want, or leave it to be automatic.
        .create();
```
If the pagesize is not set, the lib will calculate the size when opening the GUI.  
In this example we use pageSize 45


# Creating the navigation

To create the navigation items we can simply do:

```java
// Previous item
paginatedGui.setItem(6, 3, ItemBuilder.from(Material.PAPER).setName("Previous").asGuiItem(event -> paginatedGui.previous()));
// Next item
paginatedGui.setItem(6, 7, ItemBuilder.from(Material.PAPER).setName("Next").asGuiItem(event -> paginatedGui.next()));
```
It is recommended to add a default click action to your GUI to cancel the click when working with pagination, if not, make sure to cancel the click before calling `PaginatedGui#next/previous`.

# Populating the page

To add items to the page once again we use the `PaginatedGui#addItem` which takes a `GuiItem`.  
Items added with `PaginatedGui#setItem` will not be counted towards the page but as static GUI items.
