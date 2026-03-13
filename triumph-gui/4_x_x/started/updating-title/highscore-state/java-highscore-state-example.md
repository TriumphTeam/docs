Because we are out of the builder, the state creation won't be using the `remember` method but instead 
using the `MutableState.of` method.

```java
// Once again we start the state at 0.
final var highScoreState = MutableState.of(0);
```
