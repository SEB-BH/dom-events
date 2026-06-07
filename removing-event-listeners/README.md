<h1>
  <span class="headline">DOM Events</span>
  <span class="subhead">Removing Event Listeners</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to implement the removal of event listeners in the Document Object Model (DOM). 

It's possible to remove an added event listener; however, this only works if a named function was used as the callback:

```javascript
btnElement.removeEventListener('click', handleClick)
```

This would remove the `'click'` event listener (`handleClick`) that was originally registered on the `btnElement` element like this:

```javascript
btnElement.addEventListener('click', handleClick)
```

We can see how this would work by adding the logic to remove our established event listeners in the `handleReaction` callback function. Below you will find callback with our `removeEventListener` logic added:

```javascript
const handleReaction = (event) => {
  if (event.target.id === 'like-button') {
    likesCount = likesCount + 1;
    likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
    // remove the event listener from our like button
    likeButtonElement.removeEventListener('click', handleReaction);
  } else {
    dislikesCount = dislikesCount + 1;
    dislikeButtonElement.textContent = 
      `${dislikesCount} dislike(s). Dislike this post!`;
    // remove the event listener from our dislike button
    dislikeButtonElement.removeEventListener('click', handleReaction); 
  }
};
```

Note that when we click the like or dislike button after adding our `removeEventListener` logic to our buttons we only see the like count or dislike count go up one time. A second click to either button does nothing now because those elements no longer have the `handleReaction` event handler associated with them.
