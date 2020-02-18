# Unit 6 Lesson 1 Practice: Promises

## Directions
Fork and clone this lab. Respond to questions in clear, concise sentences directly within this markdown file.

**1. What will the following code snippet log? Why?**
  ```javascript
  console.log('Line 1')
  setTimeout(() => console.log('Line 2'), 1000)
  console.log('Line 3')
  ```
- Line 1 and Line 3 will print automatically, while it takes an extra second for Line 2 to print. This is because there's a set time where the program waits for a certain amount of time before activating the callback function in setTimeout.

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
- It returns a pending Promise, which has a value of undefined. If 1,000 seconds were to pass, then the value would be replaced with the sentence inside resolve. We're returning a new Promise object, which takes in a function to be executed, and you can return a resolve and a reject, which will return something if it was successful or if there was an error.

**3. How do we use our `createPromise` function to log `"After 1 second(s), this promise is resolved."`**
- Instead of passing in 1,000 in our createPromise function, pass in 1 instead. It might say it's pending when you first call the function, but if you check, it'll actually say it's resolved, and have a string for a value.

**4. What does the following code snippet return? What does it log?**
  ```javascript
  const ourPromise = new Promise((resolve) => {
    resolve(12);
  })

  ourPromise.then(value => value * 2);
  ```
- It returns a Promise object, and it's resolved with a value of 24. We call ourPromise first, which returns 12 because the Promise successfully returned it. Promises have a then method, where after a Promise is successful, you can manipulate what it returns. In this case, it takes 12, then multiplies it by 2 and returns 24.

**5. What does the following code snippet return? What does it log?** <br> _**Note:** Instead of using the `Promise` constructor to create a Promise that immediately resolves to 12, we can just use the [`Promise.resolve`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) method._
  ```javascript
  const ourPromise = Promise.resolve(12);
  ourPromise.then(value => value * 2).then(value => value + 10);
  ```
- It returns a Promise object that is resolved and has a value of 34. The Promise.resolve method is a quick way to return a successful Promise, instead of writing out the function. This is useful if you're simply returning something instead of manipulating anything that's passed in the Promise. The then method takes that returned resolve, multiplies it by 2, and returns 24. Then, another then method takes that 24 and adds 10 to it, returning 34.

**6. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => console.log(value + 10))
  ```
- The code snippet returns a 34 to the console, as well as a Promise object that is resolved, but has a value of undefined. This differs from the previous question because not only is the code snippet more elegant and all taking place in one line, it's also returning a log to the console. When you have a console log, you're putting the information to the console, which means the Promise doesn't have a value to return. The Promises had a value before, but now, it's undefined because the value is instead logged to the console.

**7. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    });
  ```
- It returns 34 to the console, as well as a Promise object that is resolved and also has the value of 34. This differs from the previous question because unlike before, now the Promise has a value, and this is because you're returning the same thing you're logging.

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
- It returns a console error, saying that 12 is a bad number, as well as a Promise object that is resolved and has a value of 12. This differs from the previous questions because now, we have a catch method, which is what will run when there is an error or a rejection. In this case, we're calling the reject method which will completely ignore all then methods and go straight to the catch method. 12 becomes the reason for the error, and a message is printed to the console. You're also returning the reason, 12, in the Promise object.