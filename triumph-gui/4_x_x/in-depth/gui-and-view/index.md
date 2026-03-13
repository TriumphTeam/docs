# The basic concepts

The main concepts of the library that you'll need to understand are: GUI, View, Component, and State.
With these concepts alone you'll be able to create any GUI you want.  
Let's start of with the main ones.

# GUI

The GUI instance is the blueprint element, which defines the structure and behavior of a GUI. 
It contains all components and states, but doesn't do anything. 
Its sole purpose is to create a new view when opening to a player. The GUI is also immutable; once built, 
the components and states added to the GUI cannot be changed.

# View

The View represents a single active instance of a GUI being displayed to a specific player. It's the stateful
representation of a GUI for one viewer. When state values bound to the View are updated, it will automatically re-render
the affected components. The View maintains a reference to its parent View (a view can be passed when opening a GUI),
which allows for navigating between views.  
Once the GUI is built, you'll be mostly interacting with the view.  
Although a view is made specifically for a player, it doesn't mean that the states are unique. If the state is shared
between multiple views, it will be updated for all views.

!!!!
Avoid storing instances of the view, as it is used as a weak reference for states to know where to trigger re-renders.
Holding the instance will prevent it from being garbage collected, which can lead to memory leaks and unexpected
behavior.
!!!
