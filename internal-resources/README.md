<h1>
  <span class="headline">DOM Events</span>
  <span class="subhead">Instructor Guide</span>
</h1>

Follow the lesson order. **Add** means new code; **Replace** means overwrite the earlier version, rather than adding another listener or function. Code blocks are copied unchanged from the attached lesson.

Keep element selections and count variables above the handlers that use them. Keep named handlers above listeners that use them. **🎓 You Do** marks a student pause; the lesson supplies tasks, but no solution snippets.

**Core:** [Setup](#1-setup) · [Concepts](#2-concepts) · [Fundamentals](#3-fundamentals) · [Responding to Events](#4-responding-to-events) · [Named Callbacks](#5-named-callbacks) · [The event Object](#6-the-event-object)

**Level Up:** [Event Bubbling](#7-event-bubbling-level-up) · [Removing Event Listeners](#8-removing-event-listeners-level-up) · [Alternate Event Listener Techniques](#9-alternate-event-listener-techniques-level-up)

## 1. Setup

_“Now we’re going to set up the HTML, CSS, and JavaScript for a small blog page.”_

**Terminal:** Open the terminal and go to the lectures folder.

```bash
cd ~/code/ga/lectures
```

Create and enter the project folder.

```bash
mkdir dom-events
cd dom-events
```

Create the JavaScript and CSS folders.

```bash
mkdir js css
```

Create the three files.

```bash
touch index.html ./js/app.js ./css/style.css
```

Open the project in VS Code.

```bash
code .
```

**`index.html`:** Type `!`, then press `Tab` to generate the HTML boilerplate.

**Add inside `<head>`:** Link the JavaScript file.

```html
<script defer src="./js/app.js"></script>
```

**Add inside `<head>`:** Link the CSS file.

```html
<link rel="stylesheet" href="./css/style.css">
```

**`css/style.css` — Add:** Starter styles.

```css
body {
  font-family: system-ui, sans-serif;
}

div {
  background-color: darkslategrey;
  /* This makes the width of the div the width required by its content! */
  width: fit-content;
  padding: 8px;
}

button {
  margin: 8px;
}
```

**`index.html` — Add inside `<body>`:** Blog heading and reaction buttons.

```html
  <h1 id="main-title">DOM Events Blog Post</h1>
  <p>DOM Events are the key to interactivity!</p>
  <div>
    <button id="like-button">Like this post!</button>
    <button id="dislike-button">Dislike this post!</button>
  </div>
```

**Check:** Open `index.html` in the browser.

## 2. Concepts

_“Let's learn what events are and how user actions can trigger our code.”_

No code changes. Briefly look at the [MDN event reference](https://developer.mozilla.org/en-US/docs/Web/Events).

## 3. Fundamentals

_“Now we’re going to make a button listen for a click and run some code when it happens.”_

**File:** `js/app.js`

**Add:** Select the like button and inspect it.

```javascript
const likeButtonElement = document.querySelector('#like-button');

// let's log it to confirm
console.dir(likeButtonElement);
```

**Check:** Confirm the correct button in the console, then remove `console.dir(likeButtonElement);`.

**Add:** Listen for a click on the like button.

```javascript
likeButtonElement.addEventListener('click', () => {
  console.log('You clicked me!');
});
```

**Check:** Open DevTools and click the like button. The console should show `You clicked me!`.

## 4. Responding to Events

_“Now we’re going to collect text from an input, create a comment, and add it to the page.”_

**`index.html` — Add below the existing `<div>` in `<body>`:** Comment list, input, and button.

```html
  <h2>Comments</h2>
  <ul>
    <li>Reading is what? Fundamental!</li>
  </ul>
  <h3>Add a comment</h3>
  <input>
  <button id="comment-button">Add comment</button>
```

**Remaining code in this section:** `js/app.js`.

**Add:** Select and inspect the comment button.

```javascript
const commentButtonElement = document.querySelector('#comment-button');

// let's log it to confirm
console.dir(commentButtonElement);
```

**Check:** Confirm the correct button in the console.

**Add:** Test the comment button listener.

```javascript
commentButtonElement.addEventListener('click', () => {
  console.log("I work!");
});
```

**Check:** Click **Add comment**. The console should show `I work!`.

**Replace the comment listener:** Remove the test log and create a new `<li>`. It is not on the page yet.

```javascript
commentButtonElement.addEventListener('click', () => {
  const commentElement = document.createElement('li');
});
```

**Replace the comment listener:** Give the new `<li>` placeholder text and inspect it.

```javascript
commentButtonElement.addEventListener('click', () => {
  const commentElement = document.createElement('li');
  commentElement.textContent = 'Can you hear me?'; // placeholder text
  console.dir(commentElement);
});
```

**Check:** Click **Add comment**. Inspect the new list item in the console.

**Add with the other element selections:** Select the comment list.

```javascript
const commentListElement = document.querySelector('ul');
console.dir(commentListElement);
```

**Check:** Confirm the correct `<ul>`, then remove `console.dir(commentListElement);`.

**Replace the comment listener:** Add the new `<li>` to the end of the list.

```javascript
commentButtonElement.addEventListener('click', () => {
  const commentElement = document.createElement('li');
  commentElement.textContent = 'Can you hear me?';
  commentListElement.appendChild(commentElement);
});
```

### 🎓 You Do — Select the input

- Select the `<input>` element and store it in `inputElement`.
- Use `console.dir()` to check the selection.

Before continuing, inspect the input element’s `value` property in the console.

**Replace the comment listener:** Use the text typed in the input instead of the placeholder.

```javascript
commentButtonElement.addEventListener('click', () => {
  const commentElement = document.createElement('li');
  commentElement.textContent = inputElement.value; // replace placeholder text
  commentListElement.appendChild(commentElement);
});
```

**Check:** Type a comment and click **Add comment**. It should appear in the list.

### 🎓 You Do some more!

- Prevent a new `<li>` from being created when the input is empty.
- Clear the input after adding a comment.

Students should use properties already covered in the lesson.

## 5. Named Callbacks

_“Now we’re going to move our callback into a named function, then use it to count and display likes.”_

**File:** `js/app.js`

**Add above the event listeners:** Give the like-button callback a name.

```javascript
const handleLike = () => {
  console.log('You clicked me!');
}
```

**Replace the like-button listener:** Pass the function name without calling it.

```javascript
likeButtonElement.addEventListener('click', handleLike);
```

**Temporary incorrect-code demo — Replace the listener briefly:** Show what happens when parentheses call the function immediately.

```javascript
likeButtonElement.addEventListener('click', handleLike());
```

**Check:** Refresh: the message appears immediately. Click: nothing happens. Restore the correct listener shown above, without `()` after `handleLike`.

**Add above `handleLike`:** Store the number of likes.

```javascript
let likesCount = 0;
```

**Replace `handleLike`:** Increase and log the count.

```javascript
const handleLike = () => {
  likesCount = likesCount + 1;
  console.log(likesCount);
}
```

**Replace `handleLike`:** Display the count in the button text.

```javascript
const handleLike = () => {
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

## 6. The event Object

_“Now we’re going to find out which button the user clicked, so one function can handle both likes and dislikes.”_

**File:** `js/app.js`

### 🎓 You Do — Connect both buttons

- Rename `handleLike` to `handleReaction`.
- Update the like-button listener to use `handleReaction`.
- Select the dislike button and store it in `dislikeButtonElement`.
- Add a `'click'` listener to the dislike button that also uses `handleReaction`.

**Check before continuing:** Both buttons currently increase the like count and update the like button. The next steps fix this.

**Replace `handleReaction`:** Receive and inspect the event object.

```javascript
// include the event parameter and console.dir it
const handleReaction = (event) => {
  console.dir(event);
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

**Check:** Click a button and find the `target` property in the logged event.

**Replace `handleReaction`:** Compare the clicked element with the selected like button.

```javascript
const handleReaction = (event) => {
  console.log(event.target);
  console.log(likeButtonElement);
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

**Check:** Click the like button. The console shows the same element twice.

**Replace `handleReaction`:** Remove the previous logs and inspect the clicked element’s ID.

```javascript
const handleReaction = (event) => {
  console.dir(event.target.id);
  likesCount = likesCount + 1;
  likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
}
```

**Check:** Click each button. Look for `like-button` and `dislike-button` in the console.

**Replace `handleReaction`:** Increase likes only when the like button is clicked.

```javascript
const handleReaction = (event) => {
  if (event.target.id === 'like-button') {
    likesCount = likesCount + 1;
    likeButtonElement.textContent = `${likesCount} like(s). Like this post!`;
  }
}
```

**Check:** The like button works; the dislike button does nothing yet.

**Add `dislikesCount` beside `likesCount`; replace `handleReaction`:** Give each button its own count. The snippet contains both changes.

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

**Check:** Click both buttons. Each updates only its own count and text.

## 7. Event Bubbling (Level Up) 🚀

_“Now we’re going to see how clicks travel through parent elements, then use one parent listener to handle both buttons.”_

**File:** `js/app.js`. Keep the existing HTML; the lesson’s HTML block here only repeats the button structure.

**Add the body/div selections and their listeners; replace `handleReaction`:** Log clicks as they reach the surrounding elements.

```javascript
const bodyElement = document.querySelector('body')
const divElement = document.querySelector('div')

bodyElement.addEventListener('click', () => {
  console.log('body')
})

divElement.addEventListener('click', () => {
  console.log('div')
})

const handleReaction = (event) => {

  // add a console log for the target's id:
  console.log(event.target.id)

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

**Check:** Click each button, the shaded `<div>` around the buttons, and the page body. Watch the console.

**Delegation — Replace the existing div logging listener with the shared handler; comment out the two button listeners:** Let the div handle button clicks.

```javascript
// comment out the lines attaching event listeners to your buttons
// likeButtonElement.addEventListener('click', handleReaction);
// dislikeButtonElement.addEventListener('click', handleReaction);

// make the divElement event listener call the handleReaction function
divElement.addEventListener('click', handleReaction)
```

### 🎓 You Do — Find the delegation bug

- Click the shaded `<div>` itself, rather than a button.
- Observe what changes, work out why, and fix the bug.

## 8. Removing Event Listeners (Level Up) 🚀

_“Now we’re going to remove each button’s listener after its first click, so users can only react once per button.”_

**File:** `js/app.js`.

**Starting point:** Use the final version from **The event Object**, with a direct `handleReaction` listener on each button. If you completed Event Bubbling, undo delegation first: remove the div’s `handleReaction` listener and restore the two button listeners.

**Syntax reference only:** The next two snippets use placeholder names, not the blog app’s variables.

Remove a listener using its event type and named callback.

```javascript
btnElement.removeEventListener('click', handleClick)
```

This is the matching registration shown in the lesson.

```javascript
btnElement.addEventListener('click', handleClick)
```

**Replace `handleReaction`:** Remove each button’s listener after its first reaction.

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

**Check:** Click each button twice. Each count increases only on its first click.

## 9. Alternate Event Listener Techniques (Level Up) 🚀

_“Now we’re going to look at two other ways to connect events to functions, so we can recognise them in other people’s code.”_

**Examples only:** The lesson does not supply a `submit` function or a `btnElement` selection for these snippets.

**HTML example:** Put the click handler in an HTML attribute.

```html
<button onclick="submit()">Add Comment</button>
```

**JavaScript example:** Assign the handler to the element’s `onclick` property.

```javascript
btnElement.onclick = submit
```

Continue using `addEventListener()` for the lesson app.


<hr>
<hr>

## Content

| Lesson                                                                                 | Video Time |                            Video                             | Skills                                                                                  |
| -------------------------------------------------------------------------------------- | :--------: | :----------------------------------------------------------: | --------------------------------------------------------------------------------------- |
| [Setup](./setup/README.md)                                                             |   5 min    | [Link](https://generalassembly.wistia.com/medias/8e58mzizlu) | Setting up the development environment.                                                 |
| [Concepts](./concepts/README.md)                                                       |   3 min    | [Link](https://generalassembly.wistia.com/medias/uwewzqnij2) | Understanding DOM events and their role in web page interactivity.                      |
| [Fundamentals](./fundamentals/README.md)                                               |   6 min    | [Link](https://generalassembly.wistia.com/medias/8y2ndw1ebj) | Compose event listeners with appropriate syntax.                                        |
| [Responding to Events](./responding-to-events/README.md)                               |   20 min   | [Link](https://generalassembly.wistia.com/medias/yhi7luhbh7) | Create in-memory elements and add them to the DOM.                                      |
| [Named Callbacks](./named-callbacks/README.md)                                         |   9 min    | [Link](https://generalassembly.wistia.com/medias/v4maljii1u) | Use named callback functions to make event handlers.                                    |
| [The `event` Object](./the-event-object/README.md)                                     |   14 min   | [Link](https://generalassembly.wistia.com/medias/bcgofjbiis) | Use the `event` object to allow multiple elements to share one named callback function. |
| [Event Bubbling](./event-bubbling/README.md)                                           |   11 min   | [Link](https://generalassembly.wistia.com/medias/j7tjlqrnm3) | Event bubbling and event delegation.                                                    |
| [Removing Event Listeners](./removing-event-listeners/README.md)                       |   5 min    | [Link](https://generalassembly.wistia.com/medias/tfr9ioigzr) | Removing a set event listener.                                                          |
| [Alternate Event Listener Techniques](./alternate-event-listener-techniques/README.md) |   4 min    | [Link](https://generalassembly.wistia.com/medias/o6kh2o36ka) | `.onclick()` and inline listeners.                                                      |
| **Total content**                                                                      |   77 min   |                                                              |                                                                                         |

## References

📖 [Reference Materials](./references/README.md)

## Internal

### Prerequisites

- Intro to HTML
- Intro to the DOM

### Course landing pages

- [Default Landing Page](https://ga-curriculum.github.io/dom-events/canvas-landing-pages/fallback)
- [SEB - Software Engineering Bootcamp](https://ga-curriculum.github.io/dom-events/canvas-landing-pages/seb)

### Resources

✏️ [Instructor Guide](./internal-resources/instructor-guide.md)

🎥 [Video Hub](./internal-resources/video-hub.md)

🏗️ [Release Notes](./internal-resources/release-notes.md)

---
