# Why Redux

#### Single Source Of Truth

As our **React** applications become larger, our state becomes more spread out between different components.  At a certain point, the component tree becomes a web of props and state that can obscure our view of how components are handling and sharing data with each other.

There are ways to get around this, like storing all of our state in one high level container component, but this can ultimately *increase* the complexity of your props.

**Redux** offers a different solution. It encourages storing all of the necessary data in our application in a JavaScript object *separate* from our components. 

```react
    state = {
      user: {
        name: 'Jean-Luc Picard',
        origin: 'La Barre, France, Earth',
        species: 'Human'
      },
      interests: [
        {
          name: 'Fencing',
          type: 'Sport'
        },
        {
          name: 'Flute',
          type:'Music'
        },
        {
          name: 'Hot Earl Grey Tea',
          type: 'Beverage'
        }
      ]
    }
```



Similar to component state, all our data is held in an object. The difference here is that, since Redux state is separate from the component tree, we can grab *any* part of this data for *any* component that needs it, just by connecting the component!

#### Accessing Our State

To make this state available for components to connect to, we provide access by wrapping the component tree, similar to `Router`. This gives us access to Redux functions that allow us to grab state and map the props being given to a component. Components can then read these props like normal, as though they were receiving them from a parent component.

Consequently, complex interaction between components is made easier. Take for example sibling components (rendered side by side in a parent) and cousin components (the children of sibling components). If siblings are both displaying or manipulating the same bit of shared data, without Redux, that data needs to be stored in their parent component's state. If *cousins* are sharing data, the data needs to be stored in the *grandparent* component, the closest shared 'ancestor' component.

In Redux all these interactions are structured the same way. Every component we allow can get and update state data regardless of the position of components in a tree.

#### Updating Our State

So we hold all of our data in one place and with some configuration, we can read it as props in regular React components. When we want to update that data, we must send an action, which is a set of strict instructions *we create* that **Redux** will use for how to update it.  

```react
    action = {
      type: 'ADD_INTEREST',
      newInterest: {
        name: 'Horseback Riding',
        type: 'Sport'
      }
    }
```

Any time we update the state in **Redux**, we must create an action first. This action is just a plain old JavaScript object.

These actions are also made available to components. Any component we connect will be able to modify the state using an action we've defined.

# Redux Resouces

1. [Redux Justification - Dan Abramov](https://www.youtube.com/watch?v=xsSnOQynTHs)

2. [Looking Back at Redux - Dan Abramov](https://www.youtube.com/watch?v=uvAXVMwHJXU)

   