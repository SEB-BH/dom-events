<h1>
  <span class="headline">DOM Events</span>
  <span class="subhead">The <code>event</code> Object</span>
</h1>

**Learning objective:** By the end of this lesson, students will understand the utility of the `event` object and how it can help us reuse some functionality.

## The dislike button

Let's begin with a quick refactor. So far, the `handleLike` function only handles likes (as its name accurately implies). In this lesson, we will rewrite it so that this single function handles both likes and dislikes.

### 🎓 You Do

Start by doing the following:

- Rename the `handleLike` function to `handleReaction`.
- Change the `likeButtonElement`'s event handler to use this renamed function instead of the old `handleLike` function.
- Select the dislike button in the DOM. Assign it to a variable called `dislikeButtonElement`.
- Add an event listener to the `dislikeButtonElement`. It should call the newly renamed `handleReaction` function when a `'click'` event occurs.

Note that now the `addEventListener` method on both `likeButtonElement` and `dislikeButtonElement` call the same event handler function (`handleReaction`). This is intentional, and is often an effective way to reduce the amount of code you've written.

After you've completed the above tasks, by clicking either the like or dislike button, the like count will be incremented. The text inside of the like button will also be updated. We'll fix this next!

## Like/dislike functionality overview

Now we're going to change up the `handleReaction` function so that it will work for both the like button and the dislike button. To do this, we must figure out which button the user clicked on. We don't currently have a mechanism to do this, but we do have access to one - the `event` object.

The `event` object is an argument that is automatically passed by `addEventListener` to its callback function. JavaScript does this for us "under the hood", so while we don't immediately see it, it is available to us. The `event` object holds details about the event that just occurred. To gain access to it, simply include it as a parameter in your event handler function.

Let's take a look:

```javascript
// include the event parameter and console.dir it
const handleReaction = (event) => {
  console.dir(event);
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

We have the flexibility to name the event parameter whatever we want, however, choosing `'event'` is descriptive and clear. Some developers might use shorter forms like `'evt'` or `'e'`, but regardless of the name, the parameter functions the same way. When examining the event object, you'll notice it has numerous properties. Locate the `target` property, we'll use this to get more information about what was clicked.

> In the event object, `event.target` represents the element in the DOM that triggered the event. That means it was the recipient of the user's action.

We can confirm this. Change the console.dir in the `handleReaction` function to log `event.target`, and add another to log the `likeButtonElement`:

```javascript
const handleReaction = (event) => {
  console.log(event.target);
  console.log(likeButtonElement);
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

If you click the like button, you'll see two identical elements printed to the console. That's because they're the same thing!

So we've established that `event.target` is the HTML element that we clicked on, so what we need to figure out next is how to tell the like button and the dislike button apart in our handler function. Then we can carry out conditional logic based on which button was clicked.

Luckily, we've attached something unique to each button that makes it distinguishable from every other element on the page - the value of the `id` attribute. We can access the value assigned to this attribute using `event.target`'s `id` property. Let's confirm that while also removing the `console.dir(likeButtonElement)`:

```javascript
const handleReaction = (event) => {
  console.dir(event.target.id);
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

If you click the like button, `'like-button'` will appear in the console. If you click the dislike button, `'dislike-button'` will appear in the console. This is a reliable way for us to uniquely identify elements and make decisions based on what a user has clicked! With that knowledge in hand, let's start implementing some conditional logic based on the element the user has clicked:

```javascript
const handleReaction = (event) => {
  if (event.target.id === 'like-button') {
    likesCount = likesCount + 1;
    likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
  }
}
```

Now, when you click the like button, the counter increments, and when you click the dislike button, nothing happens. So, let's make something happen!

```javascript
// add a new dislikesCount variable next to the existing likesCount
let dislikesCount = 0; 

// then use it in the event handler
const handleReaction = (event) => {
  if (event.target.id === 'like-button') {
    likesCount = likesCount + 1;
    likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
  } else {
    dislikesCount = dislikesCount + 1;
    dislikeButtonElement.textContent = 
      `${dislikesCount} dislike(s). Dislike this post!`;
  }
};
```

Now you can click on both buttons, and each only updates the data related to that button.
