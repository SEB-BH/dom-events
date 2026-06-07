<h1>
  <span class="headline">DOM Events</span>
  <span class="subhead">Named Callbacks</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to construct an event listener that calls a named function.

## Named callbacks

So far, when we've used callback functions, they've typically been anonymous or unnamed. Take the function we're using for the like button on our page:

```javascript
likeButtonElement.addEventListener('click', () => {
  console.log('You clicked me!');
});
```

This:

```javascript
() => {
  console.log('You clicked me!');
}
```

is an anonymous function. It's passed directly to the `addEventListener` method and lacks a descriptive name. However, nothing stops us from defining and using named functions as callbacks.

Check it out, let's write a new function ***above*** your event listeners:

```javascript
const handleLike = () => {
  console.log('You clicked me!');
}
```

> ❓ Why did we name this function ***handleLike***?

The naming convention for functions in JavaScript, especially those used as event handlers, is important. Functions provided as callbacks to `addEventListener` are essentially "event handlers". Naming them appropriately helps clarify their purpose. For instance, ***handleLike*** clearly indicates that this function is designed to handle the "like" action.

Bt this naming convention, we include the word **'handle'** followed by the action or event it's associated with.

Now, we can rewrite our event listener to use this function:

```javascript
likeButtonElement.addEventListener('click', handleLike);
```

Notice how we do not *invoke* `()` this function when we've provided it as a callback! Doing so would immediately call the function on page load rather than waiting for the event to trigger it.

Try the following ***incorrect*** code:

```javascript
likeButtonElement.addEventListener('click', handleLike());
```

Notice how the `console.log` is run as soon as the page is refreshed? Also, when you click the like button, nothing will happen. Always pass just the *function variable name* into `addEventListener` without the parentheses. This way, `addEventListener` has a reference to the function that it can call at the right time - with an event!

## Like functionality

Let's implement some basic "like" functionality. This code will count the times a user has clicked the like button. It's a good start to managing some data in this application.

We're going to need to keep track of the number of times the user has clicked the like button, which sounds like a great use for a variable:

```javascript
let likesCount = 0;
```

When the user clicks the "like" button, we should increment the number of likes by one:

```javascript
const handleLike = () => {
  likesCount = likesCount + 1;
  console.log(likesCount);
}
```

Now let's display that data on the page. We can do this by adding the number of likes to the button text itself. This is a common UI pattern you've probably seen on social media sites. We do this using the like button's `textContent` property:

```javascript
const handleLike = () => {
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

Very nice!
