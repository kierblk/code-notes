# Redux Map State to Props

We can use the **React Redux** library to get React and Redux talking to one another.

The **React Redux** library gives access to a component called the **Provider**. The **Provider** is a component that comes from our **React Redux** library. It wraps around our **App** component. It does two things for us. 

1. It will alert our **Redux** app when there has been a change in state, and this will re-render our **React** app.
2. ??

Using the `<Provider>` component provided by the **React Redux** library, we gave our components *the ability to be connected to the store*. However, we don't want every component re-rendering in response to every change in the state. So the **React Redux** library requires us to specify which changes to the store's state should prompt a re-render of the application. We will specify this with the **connect()** function.

#### Using the `connect()` function

For a component to be connected to the store, i.e. to be able to get data from the store's internal state and to be told to re-render and get new data when that state changes, we will use the **connect()** function made available to us by React Redux.

Remember, that we have two goals here: 

1. to only re-render our **App** component when specific changes to the state occur, and
2. to only provide the slice of the state that we need to our **App** component.

So we will need

1.  a function that listens to every change in the store and then
2. filters out the changes relevant to a particular component to
3. provide to that component. 

That's exactly what's happening here with the connect function.

The connect function is taking care of task 1, it is synced up to our store, listening to each change in the state that occurs. When a change occurs, it calls a function *that we write* called **mapStateToProps()**, and in **mapStateToProps()** we specify exactly which slice of the state we want to provide to our component. (Which takes care of task 2.) Then we have to say which component in our application we are providing this data to: you can see that we write `connect(mapStateToProps)(App)` to specify that we are connecting this state to the **App** component.   Finally this entire **connect()** method returns a new component, it looks like the **App** component we wrote, but now it also receives the correct data. This is the component we wish to export.

#### A Note on `dispatch`

We  will go into greater detail later, but `dispatch` is automatically provided by `connect` if it is missing a *second* argument. That second argument is reserved for `mapDispatchToProps`, which allows us to customize how we send actions to our reducer. Without the second argument we will still be able to use `dispatch` on any component wrapped with `connect`.

## Conclusion

We learned of two new pieces of **React Redux** middleware: **connect()** and **Provider**.  The two pieces work hand in hand. **Provider** ensures that our entire React application can potentially access data from the store. Then **connect()**, allows us to specify which data we are listening to (through mapStateToProps), and which component we are providing the data. 



