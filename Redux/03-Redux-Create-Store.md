# Redux Create Store

To add the official Redux library, install two packages:

	1. `redux`
 	2. `react-redux`

## Step 1: Setting up the Store

First things first, we'll use Redux to initialize our store and pass it down to our top-level container component.

Redux provides a function, `createStore()`, that, when invoked, returns an instance of the Redux store for us. So we can use that method to create a store. We want to import `createStore()` in our `src/index.js` file, where ReactDOM renders our application.

```react
// ./src/index.js 
import React from 'react'
import ReactDOM from 'react-dom'

import { createStore } from 'redux'

import shoppingListItemReducer from './reducers/shoppingListItemReducer.js'

import App from './App';import './index.css'

const store = createStore(shoppingListItemReducer)

ReactDOM.render(<App />, document.getElementById('root'))
```

Notice that we are importing the `createStore` function from Redux. Now, with the above set up, we *could* pass `store` down through App and we would be able to access the **Redux** store.

## Step 2: Add Provider to Create a Global Store

However, reducing the need for passing props is part of why **Redux** works well with React. To avoid passing `store` as a prop, we use the `Provider` component, which is imported from `react-redux`. The `Provider` component wraps the top level component, App, in this case, and is the only component where `store` is passed in:

```react
// ./src/index.js 
import React from 'react'
import ReactDOM from 'react-dom'

import { createStore } from 'redux'
import { Provider } from 'react-redux'

import shoppingListItemReducer from './reducers/shoppingListItemReducer.js'

import App from './App';import './index.css'

const store = createStore(shoppingListItemReducer)

ReactDOM.render(
  <Provider>
    <App />
  </Provider>, 
  document.getElementById('root')
)
```

By including the `Provider`, we'll be able to access our **Redux** store and/or dispatch actions from any component we want, regardless of where it is on the component tree.

## Step 3: Connect the Global Store to the Component Needing Access

To gain access to the `store` somewhere in our app, we use a second function provided by `react-redux`, `connect`. By modifying a component's export statement and included `connect`, we are able to take data from our **Redux** store and map them to a component's props. Similarly, we can *also* take actions, and by wrapping them in a dispatch and an anonymous function, be able pass them as props as well:

```react
// ./src/App.js 
import React, { Component } from 'react'
import { connect } from 'react-redux'

import './App.css'

class App extends Component {
  handleOnClick = event => {
    this.props.increaseCount() 
  }
  
  render() {
    return (
      <div className="App"> 
        <button onClick={this.handleOnClick}>Click</button>        					<p>{this.props.items.length}</p>
      </div>    
    )
  }
} 

const mapStateToProps = state => {
  return {
    items: state.items  
  }
}

const mapDispatchToProps = dispatch => {
  return {
    increaseCount: () => dispatch({
      type: 'INCREASE_COUNT' 
    })  
  }
}

export default connect(mapStateToProps,  mapDispatchToProps)(App)
```



## Step 4: Connect DevTools

There is this amazing piece of software that allows us to nicely view the state of our store and each action that is dispatched. The software does a lot more than that. 

Read about it here: [redux-devtools-extension](https://github.com/zalmoxisus/redux-devtools-extension). 

Every time we use the Redux library going forward, we should make sure we incorporate devtools. Otherwise, you are flying blind.

First, just Google for Redux Devtools Chrome. There you will find the Chrome extension for Redux. Please download it, and refresh Chrome. You will know that you have installed the extension if you go to your developer console in Google Chrome (press command+shift+c to pull it up), and then at the top bar you will see a couple of arrows. Click those arrows, and if you see Redux as your dropdown, you properly installed the Chrome extension. 

Second, we need to tell our application to communicate with this extension. Doing so is pretty easy. 

We change the arguments to our createStore method to the following:

```react
// ./src/index.js 
import React from 'react'
import ReactDOM from 'react-dom'

import { createStore } from 'redux'
import { Provider } from 'react-redux'

import shoppingListItemReducer from './reducers/shoppingListItemReducer.js'

import App from './App';import './index.css'

const store = createStore(
  shoppingListItemReducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ &&    window.__REDUX_DEVTOOLS_EXTENSION__()
)

ReactDOM.render(
  <Provider>
    <App />
  </Provider>, 
  document.getElementById('root')
)
```

nNotice that we are still passing through our reducer to the createStore method. The second argument is accessing our browser to find a method called `__REDUX_DEVTOOLS_EXTENSION__`. If that method is there, the method is executed.

### Summary

In this lesson, we saw how to use the **createStore()** method. We saw that we can rely on the Redux library to provide this method, and that we still need to write our own reducer to tell the store what the new state will be given a particular action. We saw that when using the **createStore()** method, and passing through a reducer, we are able to change the state just as we did previously. We were able to see these changes by hooking our application up to a Chrome extension called Redux Devtools, and then providing the correct configuration.

# Resources

1. [Redux DevTools Extension](https://github.com/zalmoxisus/redux-devtools-extension)

   