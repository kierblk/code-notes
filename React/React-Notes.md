# React Notes

These notes are a combination of Flatiron School's Software Engineering curriculum and Wes Bos' React courses.

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

## Components

```react
{ /* starship.js */ }

import React from 'react'

class Starship extends React.Component {
  
  render() {
    return (
      <p>Starships</p>
    )

  }
}

export default Starship
```

## Mounting

With React, we don't interact with the DOM the same way we would do with vanilla JS. However, there is one time we absolutely need to... When we mount the entire application to the page.

```react
  { /* index.html */ }

  <div id="root">
    { /* Empty div where we will mount the app */ }
  </div>
```

```react
{ /* index.js */ } 

import React from 'react'
import { render } from 'react-dom'
import Starship from './starship'


{ /* render() takes two things: 1. Some JSX, 2.Mounting point on the page */ }
render(<Starship />, document.querySelector('#root'))
```

## Returning Sibling Elements

The return statement is only able to return a single element (with any associated children) and NOT multiple sibling elements. However, there is now a way to do this in react.

Brand new in React 16.2.

```react
  return (
    <React.Fragment>
      <p>Worf</p>
      <p>Data</p>
      <p>Picard</p>
    </React.Fragment>
  )
```

## Comments

Comments are different in react.

Comments must be surrounded with curly braces, and utilize block commenting

```react
  { /* Comments must look like this */ }
```

As a side note, do NOT make a comment the first thing within a return statement. It will break. The error message given will not give a clear error mesage. A comment above the return statement essentially creates a sibling element. Utilize a React fragment or move the comment.

## Loading CSS into a React App

Two ways:

1. The 'typical' CSS link statment in the index.html file works fine
2. Import the CSS directly into the React (see example below)

```react
{ /* index.js */ } 

import React from 'react'
import { render } from 'react-dom'
import Starship from './starship'
import './css/index.css'

render(<Starship />, document.querySelector('#root'))
```

## Creating a Application Layout with Components

One component to rule them all.

```react
{/* App.js */ }

import React from 'react'

class App extends React.Component {
  render() {
    return (
      < Header />
      < Starship />
      < Footer />
    )
  }
}

export default App
```

## Passing Dynamic Data with Props

Props are the way we get data into a component. (Very similar to an attribute on an HTML tag.)

State - Where the data lives
Props - How it gets to where the data needs to go

