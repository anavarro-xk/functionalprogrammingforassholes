# Scope & Hoisting in Javascript

Seems to me that to start writing good javascript we have to understand the scope of the variables in javascript and how **hoisting** works.

## Variable Scope

Let see the following example:

```javascript

var name = "Bruce";

function checkName() {
    name = "Clark";
    console.log(name);
}

console.log(name); //it outputs Bruce
checkName(); //it outputs Clark

```

So far ok, we created a variable that holds the name "Bruce" and then a function uses the same variable but changes the value to "Clark".  So you hope to output Bruce first and Clark second.
But what happens if you call console.log(name) again after checkName()?

```javascript
var name = "Bruce";

function checkName() {
    name = "Clark";
    console.log(name);
}

console.log(name); //it outputs Bruce
checkName(); //it outputs Clark
console.log(name); //it outputs Clark

```

Why does the first console.log outputs Bruce and the second console.log outputs Clark?

When you run your javascript the language starts reading your code and when it finds the first var declaration, it says it is a global variable because it wasn't declared inside a function.  In javascript, every variable declared outside of a function is **global** and every variable declared inside a function is **local**.

The variable name in our example is **global** and because of it, when we use it again inside our checkName function, we modified it's global value once we execute it.

If you want to avoid this, then the best practice is to declare local variables:

```javascript

function checkName() {
    var name = "Bruce";
    console.log(name);
}
checkName(); //outputs Bruce
console.log(name); //outputs undefined

```

## Rules for declaring variables

### Local Variables have priority over Global Variables

If you declare a global variable and a local variable with the same name, the local variable wins:
```javascript

var name = "Bruce";

function users() {
    var name = "Clark";
    console.log(name);
}

users(); //outputs Clark

```

### Any variable declared or initialized outside a function is a global variable and available to the entire application:

```javascript
var myName = "Clark";
myRealName = "Kal-El";
```
or

```javascript
var myName;
myName;
```

### If a variable is initialized (assigned a value) without first being declared with the var keyword, it is automatically added to the global scope becoming thus a global variable:

```javascript
function showAge() {
    age = 90;
    console.log(age);
}

showAge(); //outputs 90
console.log(age); //outputs 90
```

### Javascript does not have block-level scope

```javascript
var name = "Clark";
{
    var name = "Kal-El"
}

//The second declaration of name simply re-declares and overwrites the first one
console.log(name); //outputs Kal-El
```

### setTimeout Variables are executed in the Global Scope
```javascript
var highValue = 200;
​var constantVal = 2;
​var myObj = {
    highValue: 20,
    constantVal: 5,
    calculateIt: function () {
 setTimeout (function  () {
    console.log(this.constantVal * this.highValue);
}, 2000);
    }
}
​
myObj.calculateIt(); // outputs 400​
```

___

## Hoisting

Hoisting is a concept created by developers to help explain what happens during parse phase, when variables and function declarations are moved (or hoisted) to the top of their **containing scope**.  
Before we continue, I want to make clear there are 2 phases when we execute a javascript code.  The first is known as the **parsetime** phase; in this phase the code is read and the Abstract Syntax Tree is created.  The second is the **runtime** phase, here is where the code shows the cool behaviour you programmed.

One great article where you can read about hoisting is [John Dugan's article: hoisting in javascript](https://john-dugan.com/hoisting-in-javascript/)

To make things shorter and simpler I will create a brief code snippet and explain what happens during parsetime.  If you wish for a more complex example, read John Dugan's article.

```javascript
var heroes = ["Batman", "Superman", "Green Lantern", "Cyborg"];

var pickFight = function() {
    villains = ["Mongul", "Bane", "Parallax", "Krona"];
    var fight = heroes[Math.floor(Math.random()*4)] + " vs " + villains[Math.floor(Math.random()*4)];
    return fight;
}

pickFight();

console.log(heroes[0]); //outputs Batman
console.log(villains[0]); //outputs Mongul
console.log(fight); //Error fight is not defined
console.log(pickFight()); //Doesn't get executed due to error
```

At parsetime this is what the javascript code would look like:

```javascript
var heroes;
var pickFight;
var villains;

heroes = ["Batman", "Superman", "Green Lantern", "Cyborg"];
villains = ["Mongul", "Bane", "Parallax", "Krona"];
pickFight = function() {
    var fight;
    fight = heroes[Math.floor(Math.random()*4)] + " vs " + villains[Math.floor(Math.random()*4)];
    return fight;
}

pickFight();
```
First javascript will declare all the global variables and then will assign the values.
Since villains didn't have the var keyword when it was declared inside the function, javascript will interpret the variable as global.  This completely differs from  fight which was declared inside the function using the var keyword.
The pickFight variable has the same behaviour even though it contains an anonymous function (function expression).  **If** it were instead a function declaration, the function would be hoisted to the top of the code.
```javascript
//Code with function declaration

var heroes;
var villains;

heroes = ["Batman", "Superman", "Green Lantern", "Cyborg"];
villains = ["Mongul", "Bane", "Parallax", "Krona"];
function pickFight() {
    var fight;
    fight = heroes[Math.floor(Math.random()*4)] + " vs " + villains[Math.floor(Math.random()*4)];
    return fight;
}

pickFight();
```

Hope this article helped you a little bit.  Don't feel bad if you have more questions than answers right now, it is a clear symptom that you are learning.
