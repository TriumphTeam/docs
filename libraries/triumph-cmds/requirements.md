<center><h1>Requirements</h1></center>
<center>
<p>Command Requirements</p>
</center>

---

# Requirements
Requirements give fine control to determine whether or not a sender is allowed to run a command.

## Example of requirements
Firstly, we need to register the requirement.
```java
commandManager.registerRequirement(RequirementKey.of("example"), (sender) -> {
    // requirement logic here
    return hasPermission(sender);
    })
```

Now we need to add the requirement to our command.
```java
@Requirement("example")
void execute(Sender sender) {
     // command logic here
}
```
## Additional Info
* Multiple requirements can be added to a command by wrapping them in a `Requirements` annotation.
* A `MessageKey` can be used in the requirement to send messages to the user upon not meeting the requirement. add the message key string to the parameters!
* Requirements can be inverted by adding a `boolean` to the annotation.
