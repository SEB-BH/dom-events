# Review and Knowledge Checks

This section provides questions that can be used in various teaching formats. They are suitable for integration into lectures, Slack polls, Learning Management System (LMS) checkpoints, or as part of unit assessments.

## Fundamentals

❓ Review Questions

- Which of the following is not a part of the syntax for creating an event listener?
  - The element on which the event occurred
  - The kind of event that took place?
  - The callback function that is executed in response to the event
  - The time at which the event occurred
- How many arguments does `addEventListener` accept?
- Where have we seen callback functions before?

## Responding to Events

❓ Review Questions

- True or false: manipulating the DOM in response to an event is just like manipulating the DOM normally
- What is the key of the property on input elements for getting the value of whatever the user has entered?
- Is it better to write code in small chunks, checking along the way, or to write it all at once and test to see if it works once you're done?

## Named Callbacks

❓ Review Questions

- Which of the following is correct syntax for passing a named callback to `addEventListener`:
  - `likeButtonElement.addEventListener('click', handleLike());`
  - `likeButtonElement.addEventListener('click', handleLike);`
- True or false: when you assign a function to a variable, it becomes a named function
- True or false: the following code passes `addEventListener` an anonymous function:

```javascript
likeButtonElement.addEventListener('click', () => {
  console.log('You clicked me!');
});
```

## The event Object

❓ Review Questions

- True or false: we must name the parameter in our callback function `event`. Other names like `evt`, `e`, or even `foo` will result in errors!
- What property of `event` gives us the element on which the event occurred?
- True or false: each event handler function can be assigned to one and only one element/event. You cannot pass two different invocations of `addEventListener` the same named event handler function.
