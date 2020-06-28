# Redux Action Creators

Actions are just **Plain Old JavaScript Objects** (POJOs), but that doesn't mean we should ignore them. In this section, we'll discuss the properties of actions, and how to use functions to create actions.

# Purpose of Actions

So as you know, we've been dispatching actions to our store to indicate the changes we would make to our state. In this way, actions almost feel like the request object or the parameters hash that you would see in a web application like Ruby on Rails.  

In **Rails**, a user clicking on a link kicks off a request, and that request is ultimately passed to the controller, who then has the option of changing the database. In **Redux**, a user may click on a button which dispatches an action, and the reducer would take information from that action to change the state.

# Structuring Actions

Now an action is simply a POJO that has a property of type. The reducer uses this type property to see what it should do. 

```react
    const increaseCount = {
      type: 'INCREASE_COUNT' 
    }
```

Now one can simply dispatch this action, for it to be handled by the reducer.

```react
    store.dispatch(increaseCount)
```

Remember that the store has a dispatch action, which passes the action to the reducer, who then runs its switch state to decide what to do.

# Action Creators

```react
function increaseCount() {
  return {
    type: 'INCREASE_COUNT' 
  }
}
 
store.dispatch(increaseCount())
```

in the above lines of code we define a function called `increaseCount()` whose job it is to return an action. Then we execute the `increaseCount()` function, who returns that action, and we dispatch that action to the store. If you think that this is equivalent to `store.dispatch({ type: 'INCREASE_COUNT' })`, you are right.  

We prefer wrapping our actions in a function, because oftentimes our actions have some parts that will need to change, and a function comes in handy.  For example:

```react
    function addTodo(todo) {
      return {
        type: 'ADD_TODO',
        todo: todo
      }
    }
```

So in the above function, we can imagine generating actions with different payload properties depending on what we pass to the addTodo function.

