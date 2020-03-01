# [Changing the DOM with DevTools and JavaScript](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/changing-the-dom-with-dev-tools-and-javascript)

## Learning Goals

  ### 1. Demonstrate viewing the DOM through Chrome DevTools

    Chrome: Open Developer Tools, click "Elements"
    Firefox: Right click, select "Inspect Element", click "Inspector"

  ### 2. Select an element with Chrome DevTools

  Click on the element you wish to select, the line will highlight.

  ### 3. Delete an element with Chrome DevTools

  Once selected, you can press "delete" on your keyboard.

  ### 4. Demonstrate that the source is not changed when the DOM is

  View the page source after deleting an element. The HTML is just as it was before you deleted that element. In fact, the element you deleted is still visible.

  Changes in the DOM do not affect the HTML on the server. The HTML is unchanged.

  Refreshing the browser will restore the element you delted.

  ### 5. Demonstrate opening the DevTools' JavaScript console

  Repeat the same steps to open the browser DevTools, but this time click the "console" tab.

  >`disclosure triangle` is the triangle on the left side of whatever object you are inspecting. It is hiding HTML that wouldn't normally be shown. It is good information to have if you wanted more details about what is going on behind the scenes. Those triangles are standard for hiding more information. Feel free to click on them, you can't break anything.

  ### 6. Select an element with JavaScript

  In the console, type:

  ```JavaScript
  document.querySelector('header')
  ```

  This will return something like `<header class="site- header">...</header>`.

  Clicking on the disclosure triangle will show you the full DOM node, a JavaScript object. This means we can call methods on it and utilize method chaining.

  ### 7. Delete an element with JavaScript

  ```JavaScript
  document.querySelector('header').remove()
  ```

  ### 8. Demonstrate that the source is not changed when the DOM is

  Follow the same process we followed earlier to verify that the source has not changed. To restore it, simply refresh the page (i.e. reload the DOM).

  
