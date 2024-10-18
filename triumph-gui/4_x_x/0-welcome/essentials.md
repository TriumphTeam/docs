<center><h1>Essentials</h1></center>
<center><p>A quick rundown of the main concepts used in the library.</p></center>

---

# Before you start
There are a few concepts you'll read throughout this documentation that are important to keep in mind,
they'll also be better described on their own page.  

The most important part of the library is "Components" and "States" components may or may not be linked to a state,
but if it is then updating the state will cause the component to re-render.  
The concept of "re-rendering" in here can be different from where it is done too. For example, the title can re-render 
which will re-create a new title, while a component re-rendering means it'll re-place items in the inventory.

All parts of the more internal functionality in the library can be customized as each part is tied to their own "handler".  
A component has its component renderer, the title has a title renderer, clicks have click handlers.  
You can customize the handlers per gui, globally, or even per component, depending on which part it is.
