# Redux Flow

So far we know that all of our state is in a JavaScript object, and that our actions are in another JavaScript object called an action. 

But how does an action update state?

## Functions to the Rescue

it is customary to use a `switch case` statement.

```react
// Reducer

function changeState(state, action){  
  switch (action.type) {
    case 'INCREASE_COUNT':
      return {
        count: state.count + 1
      }  
  }
}
```

This makes it very explicit and clear that `action.type` is the information we are switching on to make our decision on how to change the state.

It is important that when we change the state we never return `null` or `undefined`. We'll cover this by adding a `default` case to our function.

```react
// Reducer

function changeState(state, action){
  switch (action.type) {
    case 'INCREASE_COUNT':
      return {
        count: state.count + 1
      }
     case 'DECREASE_COUNT':
      return {
        count: state.count - 1
      }
    default:
      return state  
  }
}
```

This way, no matter what, when accessing the Redux state we'll always get some form of the state back.

To summarize:

```reStructuredText
Action -> Reducer -> Updated State
```



## Reducers are pure functions

An important thing to note about reducers is that they are pure functions. Let's remember the characteristics of pure functions:

1. Pure functions are only determined by their input values
2. Pure Functions have no side effects. By this we mean pure functions do not have any effect outside of the function. They only return a value.



## Summary

1. We hold our application's state in one plain old JavaScript object, and we update that state by passing both an action and the old state to our reducer. Our reducer returns to us our new state.
2. So to change our state we (1) create an action (an **action** is just a plain  object with a type key); and (2) and pass the action as an argument when we call  the **reducer** (which is just a function with a switch/case statement). This  produces a new state.
3. Our reducer is a pure function which means that given the same arguments of state and action, it will always produce the same new state. Also it means that our reducer never updates the previous state, but rather creates a new state object.