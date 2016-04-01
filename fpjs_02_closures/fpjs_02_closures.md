# Closures

Closures and Variable Scope are strongly related, it is not possible to talk about Scope if you don't know about variable scope, so if you haven't read the previous article about Variable-Scope](https://github.com/juanfevasquez/functionalprogrammingforassholes/tree/development/fpjs_01_variable-scope), please do so.

## What is a Closure

Closure refers to the variable scope.  In the javascript scope we have global and local variables.  Understanding when a variable is accesible is key to manipulating scope and creating cool looking javascript like a Module Pattern.
Let's see:

```javascript

function userInformation() {
    var userPass = "asdf1234";

    return {
        userValidate: function(password) {
            return (password === userPass) ? console.log("You are a valid user") : console.log("Invalid user");
        }
    }
}

var joe = new userInformation();
console.log(joe.userValidate("jkl123")); //outputs Invalid user
```

As you can see we have no global variables.  We have a function declaration and inside it we have userPass.  This userPass contain very important and **private** information, so declaring this function **inside** the function seals it.  Kind of cool stuff, by understanding closures we can now protect information.

Remember, functions within functions deal with the variable scope like this:
```javascript

function parentFunction() {
    var parentVal = "Donkey";

    function childFunction() {
        var childVal = "Didi";
        var combo = childVal + " " + parentVal;
        return combo;
    }

    console.log(childVal);
}

parentFunction();

```
If you execute the code, you will get an error saying childVal is not defined.
That is because the parentFunction doesn't have access to the variables declared inside childFunction, because childFunction is a closure, hence not allowing it's private data to be accessed from outside.

The opposite happens if we try to access parentVal from inside childFunction.  childFunction inherits the parentFunction scope (inherits its variables)

```javascript
function parentFunction() {
    var parentVal = "Donkey";

    function childFunction() {
        var childVal = "Didi";
        var combo = childVal + " " + parentVal;
        return combo;
    }

    console.log(childFunction());
}

parentFunction();//outputs Didi Donkey
```
Hope that you knowing what a closure is used for will help you undertand some design patterns that will allow you to write very clean code.
