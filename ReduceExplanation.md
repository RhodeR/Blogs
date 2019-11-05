
## What is reduce and why should I use it?
Reduce iterates over each value of an array, and reduces it to a single value, which could be anything. 
There are lots of use cases where reduce comes in handy, for example when you need to: 
- calculate the sum of your array
- calculate  the average of your array
- calculate  the biggest number of your array
- calculate  the longest word of your array
- count how many times each item is present in the array. 

## The basics
You might be familiar with the reduce syntax from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Syntax):

`arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])`

 A tear came out of your eye and you even might consider switching careers. Don't worry; you are not the only one who didn't understand the syntax immediately. The good news: it's way easier than it looks. With the reduce function you can get the same thing done as with the good old for-loop, only in one line! Also, with a for-loop data is mutated or side effects are introduced. Reduce is born from adopting functional programming, so no side effects and mutations of the original data. Take a look at the for-loop and the reduce function in the snippets below, where we add up each value of the array.  The `myArray[i]` variable in the for loop is comparable with the `arrayVal` of the reduce function. The count variable in the for-loop example underneath is comparable with the accumulator variable in the reduce function. The accumulator accumulates the returned values of the callback functions. 
 
 
```javascript
const myArray = [2, 3, 4, 5, 6]
let count = 0;

for (let i = 0; i < myArray.length; i++) {
  count = count + myArray[i] 
}

// => count = 20 
```

```javascript
const myArray = [2, 3, 4, 5, 6]

let reduced = myArray.reduce((accumulator, arrayVal) => arrayVal + accumulator);

// => accumulator= 2; arrayVal = 3  
// => accumulator= 5; arrayVal = 4  
// => accumulator= 9; arrayVal = 5  
// => accumulator= 14; arrayVal = 6  
// => reduced = 20
```


## Common mistake when using reduce for the first time
The results of both snippets above are the same, but there are some important differences. Take a look at the next snippet: 

```javascript
const myArray = [2, 3, 4]
let reduced= myArray.reduce((accumulator, arrayVal) => accumulator + arrayVal * 3); 

 // => accumulator = 2; arrayVal = 3 
 // => accumulator = 5; arrayVal = 4
 // => reduced = 23
```

Wait, what happened? The mathematicians noticed immediately: 'This isn't right'. When you take a look at the callback function this is what you expected:<br>  2 * 3 = 6 <br> 6 + 3 * 3 = 15 <br>  15 + 4 * 3 = 27. <br> <br>
But value of the variable 'reduced' is 23... Why? More tears...! When you take a look at the console.logs of the callback function it's becoming clear that the callback function isn't executed for the first value in the array. The reduce function takes that first arrayValue as the initial value, which gives the following calculation: 
<br> 2 + 3 * 3 = 11 <br>
11 + 4 * 3 = 23<br> <br>

Okay, fine, when I really have to accept that for the first arrayValue the callback function is not executed, I will accept it. But sometimes you want the callback function to be executed for **every** value in the array. 

## InitialValue to the rescue
In that case you are able to use the initialValue of the reduce function, as is shown in the snippet below. 


```javascript
const myArray = [2, 3, 4]
let reduced = myArray.reduce((accumulator, arrayVal) => accumulator + arrayVal * 3, 0); 


 // => accumulator = 0; arrayVal=2
 // => accumulator = 6; arrayVal=3  
 // => accumulator = 15; arrayVal=4  
 // => reduced = 27
```

Do you see what has changed? In the code above there is a zero after the callback function; the initialValue. Now the callback function is invoked three times as you would expect. <br>
0 + 3 * 2 = 6 <br>
6 + 3 * 3 = 15 <br> 
15 + 4 * 3 = 27 

So when should you use the initial value? If you want to iterate over each value in the array with a callback function, where the callback function not only includes adding up the arrayValue with the accumulator, then you should use the inital value. 

## Why and how to use index 
There's one more important issue to address. Sometimes you want to execute different calculations for each value in the array. 
For example: you want to multiply each of your arrayValues with the index of the arrayValue. In the classic for-loops you were able to do this: `myArray[i]`. With the reduce function you are able to use the optional index value, which can be used as shown in the snippet:

```javascript
const myArray = [2, 3, 4]
let reduced = myArray.reduce((accumulator, arrayVal, i) => accumulator + arrayVal * i, 0); 


// => accumulator = 0   arrayVal = 2   i = 0
// => accumulator = 2   arrayVal = 3   i = 1
// => accumulator = 5   arrayVal = 4   i = 2
// => reduced = 13
```

See, that's it. 

## Summary
- Reduce iterates over each value of an array, and reduces it to a single value.
- Reduce is useful for for example calculating the average, finding the biggest number or the longest word in an array.  
- The accumulator accumulates the returned values of the callback functions. 
- The callback function is not executed for the first value of the array.
- When you want the callback function to execute for every value in the array and you want the reduce function to start with a specific value: use the optional initial value of the reduce method. 
- Use the index when the array order matters to the logic. 

Bonus 1:  Figure out why the first example doesn't need an initial value. <br>
Bonus 2:  Try it yourself. I already gave some examples in the codepen which you can alter. 

{% codepen https://codepen.io/RhodeZ/pen/wvwVddP default-tab=js %}


