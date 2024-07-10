<center><h1>ScrollingGUI</h1></center>
<center><p>Simple GUI that allows you to scroll on a Paginated GUI instead of going page by page.</p></center>

# Scrolling GUI

![](https://i.imgur.com/nadBZEL.gif)

# Creating a Scrolling GUI

To create a Scrolling GUI It's pretty straight forward:

```java
ScrollingGui gui = Gui.scrolling()
        .title(Component.text("GUI Title!"))
        .rows(6)
        .pageSize(45)
        .scrollType(ScrollType.HORIZONTAL)
        .create();
```
The scrollType if not specified will fall back to `ScrollType.VERTICAL`


Just like the normal [GUI](/gui) the first parameter is the rows the GUI should have. Like the [Paginated GUI](/pagegui) the second parameter is to specify the page size, as in how big the page should be, in the example above it's 45 slots dedicated for the page.

Everything else about this GUI is exactly like the [Paginated](/pagegui).
