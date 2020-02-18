# Unit 6 Lesson 1 Practice: Promises

## Directions
Fork and clone this lab. Respond to questions in clear, concise sentences directly within this markdown file.

**1. What will the following code snippet log? Why?**
  ```javascript
  console.log('Line 1')
  setTimeout(() => console.log('Line 2'), 1000)
  console.log('Line 3')
  ```
Answer: This code snippet will log "Line 1 , Line 3  and Line 2". Since setTimeout is an asynchronous function,  so it get placed on the web api waiting to execute and every thing else that doesn't need to wait is executed.
  

**2. What does the following code snippet log? Why?**
  ```javascript
  function createPromise(seconds) {
    return new Promise((resolve) => {
      setTimeout(function() {
        resolve(`After ${seconds} second(s), this promise is resolved.`)
      }, seconds * 1000)
    })
  }

  console.log(createPromise(1000))
  ```
Answer: This code snippet will log a promise object with a pending state and the message `After ${seconds} second(s), this promise is resolved` will only logged after 15 mins of waiting. 

**3. How do we use our `createPromise` function to log `"After 1 second(s), this promise is resolved."`**
    Answer: `createPromise(3).then(value => console.log(value))`


**4. What does the following code snippet return? What does it log?**
  ```javascript
  const ourPromise = new Promise((resolve) => {
    resolve(12);
  })

  ourPromise.then(value => value * 2);
  ```
  Answer: The following code snippet return a promise object with a resolve state because on line 36 we use our resolve callback and passed in the value 12, we then use the `thenable` method to take that value and multiply it by 2 and thats how we received the promise value 24. 

**5. What does the following code snippet return? What does it log?** <br> _**Note:** Instead of using the `Promise` constructor to create a Promise that immediately resolves to 12, we can just use the [`Promise.resolve`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) method._
  ```javascript
  const ourPromise = Promise.resolve(12);
  ourPromise.then(value => value * 2).then(value => value + 10);
  ```
Answer: The following code snippet return a resolved promise object. Instead of using `new Promises()` we used `Promise.resolve()` which return a Promise object that is resolved with a given value. If the value is a promise, that promise is returned. The returned promise will "follow" that thenable, adopting its eventual state; otherwise the returned promise will be fulfilled with the value.

**6. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => console.log(value + 10))
  ```
  Answer: The following code snippet will return a console.log of value 34 . This differ from the question above because the console.log returns undefined in our promise object but that status is resolved and the value log to the console. 
  

**7. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    });
  ```
  Answer: The following code snippet will return the vaue 34 and logs a promise object with a resolve state.

**8. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.reject(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    }).catch(reason => {
      const message = `${reason} is a bad number.`;
      console.error(message);
      return reason;
    });
  ```
  Answer: The following code snippet will return a promise object with a rejected state at first , it then ignore the first 2 then methods and executed it's catch method because this is our way to handle errors. `Catch` will return a  promise so it becomes resolve only after our catch was executed.