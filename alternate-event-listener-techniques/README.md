<h1>
  <span class="headline">DOM Events</span>
  <span class="subhead">Alternate Event Listener Techniques</span>
</h1>

**Learning Objective:** By the end of this lesson, students will be able to apply different techniques for adding event listeners in the DOM, including inline event handling and assigning functions directly to DOM element properties. 

Understanding different methods for registering event listeners is crucial. Each approach has its use cases and implications. Let's explore two additional methods beyond the commonly recommended `addEventListener()`.

The following examples demonstrate a `'click'` event:

## 1. In the HTML (inline)

```html
<button onclick="submit()">Add Comment</button>
```

This method involves directly embedding the event listener within the HTML tag. It's straightforward and easy to implement, especially for quick, small-scale projects or for beginners just starting to learn how to handle events.

However, using the HTML approach (`onclick="submit()"`) is typically frowned upon because it requires that the function be in the global scope.

Inline event handling also mixes JavaScript with HTML, which can make the code less maintainable and harder to debug. It's akin to inline CSS styling, which is generally discouraged for similar reasons.

## 2. Assigning to DOM elements' properties

Assigning a function directly to the DOM element's event property is another method.

```javascript
btnElement.onclick = submit
```

This approach (`element.onclick`) is slightly better than the HTML approach because it does not require a globally scoped function. `submit` can be a function scoped more narrowly, reducing the risk of conflicts.

It offers a better separation of HTML and JavaScript compared to inline methods, though it's still less modular than `addEventListener()`.

## Summary

In summary, while these methods have their use cases, `addEventListener()` remains the recommended practice, particularly for complex or larger-scale applications. It offers greater flexibility, better maintainability, and adheres to modern web development best practices. It's also important to recognize these alternate methods, as they are still used in various scenarios, including some older frameworks and legacy codebases.
