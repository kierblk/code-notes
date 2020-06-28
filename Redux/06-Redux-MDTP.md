# Redux Map Dispatch to Props

Just like we can write code like `connect(mapStateToProps)(App)` to add new props to our **App** component, we can pass `connect()` a second argument, and add our *action creator* as props.

#### Using `mapDispatchToProps`

To quickly review: The first argument passed into `connect()` is a function. That function is written to accept the Redux store's state as an argument and returns an object created using all or some of that state. Key/value pairs in this returned object will become values we can access in the component we've wrapped with `connect()`

When `connect()` executes, it calls the function passed in as its first argument, passing in the current state to the function.

Just like the first argument, `connect()` accepts a **function** for the *second* argument. This time, again, when `connect()` executes, it calls the second function passed in. However, instead of passing *state* in, it passes in the *dispatch* function. This means we can write a function assuming we have access to `dispatch()`. We call it `mapDispatchToProps` because that is what it does.

```react
    // src/App.js
     
    import React, { Component } from 'react'
    import './App.css';
    import { connect } from 'react-redux'
    import { addItem } from  './actions/items'
     
    class App extends Component {
     
      handleOnClick = event => {
        this.props.addItem() // Code change: this.props.dispatch.store is no longer being called
      }
     
      render() {
        return (
          <div className="App">
            <button onClick={this.handleOnClick}>
              Click
              </button>
            <p>{this.props.items.length}</p>
          </div>
        )
      }
    }
     
    const mapStateToProps = (state) => {
      return {
        items: state.items
      }
    }
     
    // Code change: this new function takes in dispatch as an argument
    // It then returns an object that contains a function as a value!
    // Notice above in handleOnClick() that this function, addItem(),
    // is what is called, NOT the addItem action creator itself.
    const mapDispatchToProps = dispatch => {
      return {
        addItem: () => {
          dispatch(addItem())
        }
      }
    }
     
    export default connect(mapStateToProps, mapDispatchToProps)(App)
```

## Alternative Method

There is an even simpler way to approach bundling our actions and `dispatch` into props. The second argument of `connect` will accept a function (as we've seen) *or* an object. If we pass in a function, `mapDispatchToProps()`, we must incorporate `dispatch` as with the previous example. If we pass in an object, `connect` handles this step for us! The object just needs to contain key/value pairs for each action creator we want to become props. In our example, we've using the `addItem` action creator, so the object would look like this:

```react
{ 
  addItem: addItem
}
```

As of JavaScript ES6, when we have an object with a key and value with the same name, we can use the shorthand syntax and write:

```react
{  addItem}
```

This is all we need to pass in as a second argument for `connect()`.

```react
    import React, { Component } from 'react';
    import './App.css';
    import { connect } from 'react-redux';
    import { addItem } from  './actions/items';
     
    class App extends Component {
     
      handleOnClick = event => {
        this.props.addItem()
      }
     
      render() {
        debugger
        return (
          <div className="App">
            <button onClick={this.handleOnClick}>
              Click
              </button>
            <p>{this.props.items.length}</p>
          </div>
        );
      }
    };
     
    const mapStateToProps = (state) => {
      return {
        items: state.items
      };
    };
     
    export default connect(mapStateToProps, { addItem })(App); // Code change: no mapDispatchToProps function required!
```

## Default Dispatch Behavior

In addition to this, as per Dan Abramov, the creator of **Redux**:

> By default mapDispatchToProps is just dispatch => ({ dispatch }). So if you don't specify the second argument to connect(), you'll get dispatch injected as a prop in your component.

# Resources

1. [Dan Abramov's Stack Overflow Response about mapStateToProps](https://stackoverflow.com/questions/34458261/how-to-get-simple-dispatch-from-this-props-using-connect-w-redux)

   