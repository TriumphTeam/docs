# Paginated GUI

![](../../.gitbook/assets/ezgif-6-90e434269b68.gif)

## Creating a Paginated GUI

To create a Paginated GUI `code` test `here` all you need to do is:

```java
// Main constructor
PaginatedGui gui = Gui.paginated()
        .title(Component.text("GUI Title!"))
        .rows(6)
        .pageSize(45) // Set the size you want, or leave it to be automatic.
        .create();
```

The page size, is how big the page should be, in the example above it's 45 slots dedicated for the page, if nothing is set the lib will calculate the page size when opening.

## Creating the navigation

To create the navigation items we can simply do:

```java
// Previous item
paginatedGui.setItem(6, 3, ItemBuilder.from(Material.PAPER).setName("Previous").asGuiItem(event -> paginatedGui.previous()));
// Next item
paginatedGui.setItem(6, 7, ItemBuilder.from(Material.PAPER).setName("Next").asGuiItem(event -> paginatedGui.next()));
```

Kotlin test
```kt
routing {

    get<Api.Summary> { location ->
        val summary = transaction {
            val project = getProject(location.project) ?: return@transaction null

            val entries = Entries.select {
                Entries.project eq project[Projects.id]
            }.orderBy(Entries.position).mapNotNull { mapEntry(it) }

            SummaryData(entries)
        } ?: run {
            call.respond(HttpStatusCode.NotFound)
            return@get
        }

        call.respond(summary)

    }

    get<Api.Page> { location ->
        val page = transaction {
            getPage(location.project, location.page)?.get(Pages.content)
        } ?: run {
            call.respond(HttpStatusCode.NotFound)
            return@get
        }

        call.respondText(page)
    }

    get<Api.Content> { location ->
        val contentData = transaction {
            val page = getPage(location.project, location.page) ?: return@transaction null

            val entries = Contents.select {
                Contents.page eq page[Pages.id]
            }.orderBy(Contents.position)
                .map {
                    ContentEntry(it[Contents.literal], it[Contents.indent])
                }

            ContentData(page[Pages.github], entries)
        } ?: run {
            call.respond(HttpStatusCode.NotFound)
            return@get
        }

        call.respond(contentData)
    }

}
```

Gradle test
```groovy
dependencies {
    implementation "joda-time:joda-time:2.2"
    testImplementation "junit:junit:4.12"
}
```

Recommended to add a default click action to cancel the click even when working with pagination, if not, then make sure the navigation item cancels the click before doing `PaginatedGui#next/previous` .

## Populating the page

To add items to the page once again we use the `PaginatedGui#addItem` which takes a `GuiItem`. Items added with `PaginatedGui#setItem` will not be counted towards the page but as static GUI items.
