<center><h1>Suggestions</h1></center>
<center>
<p>Argument Suggestions</p>
</center>

---

# Suggestions
Suggestions, as the name suggests, allow for command inputs to be suggested to the user based on the argument required.

## Registering suggestions
There are two ways to register suggestions:
The first way is to register by `Class` type. This will make all arguments using the class type use the suggestion resolver.
The second way is to register by using a `SuggestionKey`. This will only resolve suggestion when parameters are annotated with `@Suggestion`.
Both of these methods will have a second parameter of a lambda that has 2 parameters of the Sender object, alongside the `SuggestionContext` and will return a `List<String>`.

## Registering by Class

```java
commandManager.registerSuggestion(LocalDate.class, (sender, context) -> List.of(LocalDate.now(), LocalDate.EPOCH)); // suggest today's date and epoch date
```
That's all for registering with class types! Now this will be the default suggestion resolver for LocalDate arguments.

## Registering with Suggestion Keys

```java
commandManager.registerSuggestion(SuggestionKey.of("formatted-dates"), (sender, context) -> {
    var pattern = DateTimeFormatter.ofPattern("dd/MM/yyyy");
    return Stream.of(LocalDate.now(), LocalDate.EPOCH).map(pattern::format).toList(); // suggest dates in a different format
    })
```

Now that the suggestion is registered, we must annotate the argument.
```java
void execute(Sender sender, @Suggestion("formatted-dates") LocalDate date) {
    // command logic here
}
```
