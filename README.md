#### What is hoisting?

Hoisting in Javascript is a process where the Javascript interpreter appears to move the declarations of functions, variables and classes to the top of their scope before the code executes.

Hoisting allows us to safely use functions before they are used. On the other hand, while variable & class declarations are hoisted, their initializations are not. Therefore, using them before they are actually declared + initialized in code can lead to unexpected bugs/errors.

#### What is scoping 

Scoping refers to which variables, functions, and objects are accessible to your code during runtime. Scope of a variables depends upon where it is declared. Mainly, there are two types of scopes: global & local.

#### How are var, let const different?

Var is globally / function scoped while let & const are block scoped. 

Var can be re-assigned + re-declared. Let variables can be re-assigned but not re-declared. Const cannot be re-assigned nor re-declared.

While all three are hoisted, let & const are not initialized till they are actually declared in code. They stay in the Temporal Dead Zone till they are actually declared.

#### What are the two main differences in arrow functions?

- The "this" value for arrow functions is the value of its enclosing environment. This features makes arrow functions great for using as as callbacks inside methods. On the other hand, function declarations have their own 'this' value. When declared normally, "this" points to the global object or undefined (in strict mode). When declared like a method, "this" points to the object that invokes it.
- The syntax is very different. arrow functions have the syntax (a, b, c) => {a+b+c} while functions declared with the "function keywords" have the syntax as function() {return a+b+c}

#### Does Call apply bind work for arrow functions?

Since arrow functions don't have their own "this", call, apply and bind can only be used to pass in arguments and not the "this" value.

#### What does call apply bind do?

Call apply bind allow us to specify the "this" value for a function. Also, they allow us to pass in arguments to the function.

#### What are closures?

Closures are a combination of a function bundled together with its environment/surrounding state/lexical environment. In simpler words, a closure gives access to an outer function's scope from inner function.

#### Write a program to debounce a search bar?

```
<input name='search' id='searchbar' />

<script>

const searchbarElement = document.getElementById("searchbar")

searchbarElement.addEventListener("change", debouncer(search, 300));

function debouncer(fn, delay){
  let id;
  return (...args) => {
    if(id) clearTimeout(id)
    id = setTimeout(() => fn.apply(this, args), delay)
  }
}

function search(){
    return fetchSomeData()
}


</script>
```


#### Write a program to throttle search bar

```

function throttler(fn, delay = 300) {
        let flag;
        return function (...args) {
          if (!flag) {
            fn.apply(this, args);
            flag = true;
            setTimeout(() => {
              flag = false;
            }, delay);
          }
        };
      }

```

#### create a custom method for an array called myMap, use prototype chain to achieve this

```
Array.prototype.myMap = function (fn) {
  const res = [];
  for (let i = 0; i < this.length; i++) {
    let newEl = fn(this[i], i, res);
    res.push(newEl);
  }
  return res;
};
```


#### What is event bubbling?

When an event happens on an element, it first runs on the element, then on its parents and then keeps on going till its ancestor element. This process is known as event bubbling. Almost all events bubble except for a few such as the focus event.

#### What is the event loop?

Event loop is a constantly running process which keeps checking the call stack and callback queue. If the call stack is empty, the event loop will go to the callback queue. If it finds something to run in the callback queue, that function will be dequeued and the event loop will push it on top of the stack.

#### Explain promises to a 5 year old, with simple examples

Promises are objects in Javascript that represent the eventual completion (success or failure) of an asychronous task and its resulting value. Essentially, a promise is a returned object which you attach callbacks to using the "then" method, instead of passing callbacks into a function. 

To explain this simply, if some kid asks for chocolate, I will ask him to wait & go to the market to buy the chocolate. If the chocolate is available, I'll come back with it and give it to the kid, if not I'll let the kid know that it wasn't there. If I give the kid the chocolate, "then" he will be happy, if not, he will be sad (represents failure of Promise and the consequent handling of it).

#### Write a function called sleep that will return a promise, if you do not provide a number to the function, then it will return an error and goto the catch block

```

function sleep(num) {
  return new Promise((resolve, reject) => {
    if (!num) {
      reject(error);
    }

    setTimeout(() => resolve(num), num);
  });
}

```

#### What does the this keyword mean?

A property of an execution context (global, function or eval) that, in non–strict mode, is always a reference to an object and in strict mode can be any value.

#### What are classes? what are getters and setters?

Classes are templates/blueprints for creating objects. They encapsulate data with code to work on that data. Classes in JS are built on prototypes. Classes can be declared using class declarations or class expressions.

```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

Getters bind an object property to a function that will be called when that property is looked up.

Setters bind an object property to a function to be called when there is an attempt to set that property.

#### How do you declare private and static variables in classes

Private variables in classes can be declared using a hash (#) prefix. Static variables can be declared by prefixing variables with the "static" keyword.

#### Create a Calculator class, it should be able to add, reduce multiply and divide. it should have a value getter, and that should return final output. keep the history of changes made as well, and keep that private, and a user should be able to see previous changes made to the value

```
class Calculator {
  constructor(value) {
    this.value = value;
    this.history = [`Begun with ${value}`];
  }

  add(x) {
    this.value = this.value + x;
    this.history.push(`Added ${x}`);
    return this.value;
  }

  subtract(x) {
    this.value = this.value - x;
    this.history.push(`Subtracted ${x}`);
    return this.value;
  }

  multiply(x) {
    this.value = this.value * x;
    this.history.push(`Multiplied ${x}`);
    return this.value;
  }

  divide(x) {
    this.value = this.value / x;
    this.history.push(`Divided ${x}`);
    return this.value;
  }
}

let myCalc = new Calculator(5);

console.log(myCalc.add(10));
console.log(myCalc.subtract(5));
console.log(myCalc.multiply(10));
console.log(myCalc.history);

```

#### What is currying?

Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c). Currying doesn’t call a function. It just transforms it.

#### Write a program to flatten an array

```
// input: [ 1, [ 2, 3 ], [ 3 ], [ [ [ 5]],  6]  ]
// output => [ 1, 2, 3, 3, 5, 6 ]
```
