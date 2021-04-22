# JavaScript

### 1. What is JavaScript?

[JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/Dynamic_programming_language) is a [dynamic programming language](https://developer.mozilla.org/en-US/docs/Glossary/Dynamic_programming_language) that can adds **interactivity** to your website. You can use JavaScript to do a lot of things. For example :

- Browser Application Programming Interfaces ([APIs](https://developer.mozilla.org/en-US/docs/Glossary/API)) 

- Third-party APIs

- Third-party frameworks and libraries

  

### 2. Usage

- Create a new folder named `scripts` and create a new file called `main.js` in it

- In your `index.html` file, enter this code on a new line, just before the  `</body>` closing tag

  ```html
  <script src="scripts/main.js" defer></script>
  ```

- Add the following code to `main.js` 

  ```javascript
  const myHeading = document.querySelector('h1');
  myHeading.textContent = 'Hello world!';
  ```

  `querySelector()` and textContent are parts of the [Document Object Model (DOM) API](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model), which has the capability to manipulate documents.

  Use a function called `querySelector()` to grab a reference to your heading, and then store it in a variable called `myHeading`.  When you want to do something to an element, you need to select it first.

  Following that, the code set the value of the `myHeading` variable's `textContent` property (which represents the content of the heading) to *Hello world!*.

- Save HTML and JavaScript files, then load `index.html` in your browser

  

### 3. Core features of JavaScript

- **Variable** 

  We can use the **let** (recommended) or **var** keyword  to declare a variable. 

  Variables are containers that store values. If values couldn't change, then you couldn't do anything dynamic. So we need variables? Everything in JavaScript is an object and can be stored in a variable.
  
  ```javascript
  let myVariable = 'Johnson';
  myVariable = 'Steve';
  ```

| Data Types | Example                                          |
| :--------- | :----------------------------------------------- |
| String     | `let myVariable = 'Johnson';`                    |
| Number     | `let myVariable = 42;`                           |
| Boolean    | `let myVariable = true;`                         |
| Array      | `let myVariable = [1,'Bob','Steve',10];`         |
| Object     | `let myVariable = document.querySelector('h1');` |

- **Comments**

  ```javascript
  /*
  Everything in between is a comment.
  */
  
  // This is a comment
  ```

- **Operators**

  `+ - * / `, `=`, `===`, `!`，`!==`. 

  See [Expressions and operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators) for a complete list.

- **Conditionals**

  ```javascript
  //	if...else
  let iceCream = 'chocolate';
  if(iceCream === 'chocolate'){
      alert('Yay, I love chocolate ice cream!');
  } else {
      alert('Awww, but choclate is my favorite...');
  }
  ```

- **Functions**

  [Functions](https://developer.mozilla.org/en-US/docs/Glossary/Function) are a way of packaging functionality that you wish to reuse. 

  ```javascript
  let myVariable = document.querySelector('h1');
  alert('hello!');
  
  function multiply(num1,num2) {
    let result = num1 * num2;
    return result;
  }
  ```

  These functions, `document.querySelector` and `alert`, are built into the browser.

- **Events**

  Real interactivity on a website requires event handlers. These are code  structures that listen for activity in the browser, and run code in  response. 

  ```javascript
  document.querySelector('html').onclick = function() {
      alert('Ouch! Stop poking me!');
  }
  ```

  ```javascript
  //	Two equivalent ways
  document.querySelector('html').onclick = function() {};
  
  let myHTML = document.querySelector('html');
  myHTML.onclick = function() {};
  ```



### 3. Practice

- Adding an image changer

  ```javascript
  //	Add the following code to main.js
  let myImage = document.querySelector('img');
  
  myImage.onclick = function() {
      let mySrc = myImage.getAttribute('src') {
          if(myImage === 'images/firefox-icon.png') {
              myImage.setAttribute('src','images/firefox2.png');
          } else {
              myImage.setAttribute('src','images/firefox-icon.png');
          }
      }
  }
  ```

  

## Appendix

### 1. Semicolons Usage  in JavaScript

- Required

  When two statements are on the same line

- Optional

  After statements

- Aviod

  - After a closing curly bracket;
  - After the round bracket of an if, for, while, or switch statement

  You can use [JSLint](https://news.codecademy.com/your-guide-to-semicolons-in-javascript/) to fix your semicolons.



Reference

[1]:https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics
[2]:https://news.codecademy.com/your-guide-to-semicolons-in-javascript/



