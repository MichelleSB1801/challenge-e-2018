### ALGORITMOS

Escribir una función simple (no más de 100 caracteres) que retorne un boolean indicando si un string
dado es un palíndromo.
```javascript
function esPalindromo(str) 
{
    return str == str.split('').reverse().join('');
}
```

### JAVASCRIPT 

What will the code below output to the console and why?

```
outer func:  this.foo = bar
outer func:  self.foo = bar 
inner func:  this.foo = undefined 
inner func:  self.foo = bar 

because the scope of the function, in inner func: this.foo refers to a 
variable out of the function thats why it results undefined
```
```javascript
var myObject = {
    foo : "bar",
    func:function() {
        var self=this;
        console.log("outer func: this.foo = "+this.foo);
        console.log("outer func: self.foo = "+self.foo);
        (function(){
            console.log("inner func: this.foo = " +this.foo);
            console.log("inner func: self.foo = " +self.foo);   
        }());
    }
};

myObject.func();
```



a. What is a Promise?
``` 
A promise is the eventual result or failure of an asynchronous operation. 
```

b. What is ECMAScript?
```
It is the base from which different script languages come
```

c. What is NaN? What is its type? How can you reliably test if a value is equal to NaN ?
```
Not A Number, numeric data type value with an undefined value, 
using Number.isNaN() method
```

d. What will be the output when the following code is executed? Explain.

```javascript 
console.log(false=='0')
console.log(false==='0')
```

```
console.log(false=='0') = true, is not a strict comparison, will try to convert the types before compare.
console.log(false==='0') = false, this is a strict comparison, compare it's type.
```


### Node

Explain what does "event-driven, non-blocking I/O" means in Javascript.

```
In a sequential event model, it is important not to block something waiting for
a response that may take longer than expected to arrive, so to avoid blocking the
event loop you must work with promises to work the events asynchronously.
Don't ever block the event loop.
```









