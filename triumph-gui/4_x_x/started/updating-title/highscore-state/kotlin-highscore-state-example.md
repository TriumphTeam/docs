Because we are out of the builder, the state creation won't be using the `remember` function but instead
using the `mutableStateOf` function.

```kotlin
// Once again we start the state at 0.
// We also don't use "by" here, we don't want to delegate the value just yet.
// We need the MutableState instance so we can tell the title to remember it.
val highScoreState = mutableStateOf(0)
```
