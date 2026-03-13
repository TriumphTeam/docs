# Dynamic title with states

States can also be applied to titles, which means we can share them between a component and a title, making a component
update the title.  
For this example, let's add a "restart" button and a "High-score" state that we can display in the title.

## High-score state

Let's create a new state that will hold the high-score. This state will be created in a place where it
can be used in both the title and the component.
{highscore-state-example}

## Using a functional title

With the new state created, we can change how we do the title to include a state.
{title-example}

## Finalizing

Now we can change the click action of the cookie item to update the high-score state, as well as add a restart button.
Here's the full final code:
{example}
!!!
By default, states use [StructuralEquality](/TODO) as their [StateMutationPolicy](/TODO), so updating the value with the
same value will not trigger a re-render. Meaning that the title will only update when the value actually changes.
!!!

## Result

![](/static/updating-title-example.mp4)

# Next steps

Now that you have seen the examples and learned how to build a GUI, continue reading on the more in-depth aspects of the
library.
