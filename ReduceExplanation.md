## The basics
You probably have once read the reduce function on [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Syntax), with the following syntax:

**'arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])'.**

 A tear came out of your eye, in need of alcohol.. lots of it. Don't worry; you are not the only one who didn't understand the syntax immediately. The good news: it's way easier than it looks. With the reduce function you can get the same thing done as with the good old for loop, only in one line! Take a look at the for loop and the reduce function in the snippets underneath. The count variable in the for loop is comparable with the count variable in the reduce function, the 'myArray[i]' variable in the for loop is comparable with the 'arrayVal' of the reduce function, it's that easy. In the code examples below I renamed the variable 'accumulator' which is used in de MDN syntax of reduce, to 'count', cause 'accumulator' is a terrible abstract word. With 'count' it's easier to understand what's happening and you can see the simularity with the for loop. 


```javascript
const myArray = [2,3,4,5,6]
let count=0;

for (let i = 0; i<myArray.length; i++) {
count = count + myArray[i] 
}

// count = 20 
```

```javascript
const myArray = [2,3,4,5,6]

let reduced=myArray.reduce((count, arrayVal) => arrayVal + count );

//count= 2 arrayVal= 3  
//count= 5 arrayVal= 4  
//count= 9 arrayVal= 5  
//count= 14 arrayVal= 6  
//reduced = 20
```

The results of both snippets are the same, but there are some important differences. Look at the snippet underneath. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((count, arrayVal) => count + arrayVal * 3); 

 // => count=2   arrayVal=3, 
 // => count=5   arrayVal=4,
 // => reduced=23
```

What? What happened? The mathematicians noticed immedeately: 'This isn't right'. When you take a look at the callback function this is what you expected:<br>  2 * 3 = 6 <br> 6 + 3 * 3 = 15 <br>  15 + 4 * 3 = 27. <br> <br>
But value of the variable 'reduced' = 23... Why?? Another tear... When you take a look at the console.logs of the callbackfunction it's very clearly that the callback function isn't executed for the first value in the array. The reduce function takes that first arrayValue as the initial value, which gives the following calculation: 
<br> 2 + 3 * 3 = 11 <br>
11 + 4 * 3 = 23<br> <br>

Okay.. fine, when I really have to accept that for the first arrayValue the callback function is not executed, I will accept it. But sometimes you want the callback function to be executed for **every** value in the array. 

## InitialValue to the rescue
In that case you are able to use the initialValue of the reduce function, as is shown in the snippet below. 


```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((count, arrayVal) => arrayVal * 3, 0); 


 // => count=0   arrayVal=2
 // => count=6   arrayVal=3  
 // => count=15   arrayVal=4  
 // => reduced=27
```

See what is changed? In the code above there is a zero after the callback function; the initialValue. Now the callback function is invoked three times as you would expect. <br>
0 + 3 * 2 =6 <br>
6 + 3 * 3 = 15 <br> 
15 + 4 * 3= 27 

## Why and how to use index 
One more important issue to address. Sometimes you want to execute different calculations for each value in the array. 
For example: you want to multiply each of your arrayValues with the index of the arrayValue. In the classic for loops you were able to do this by: myArray[i]. With the reduce function you are able to use the optianal index value, which can be used as shown in the snippet below. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((count, arrayVal, i) => count + arrayVal * i, 0); 


// => count=0   arrayVal=2   i=0
// => count=2   arrayVal=3   i=1, 
// => count=5   arrayVal=4   i=2
// => reduced=13
```

See, that's it. 

Summary
- The initial value of the reduce function is the first value of the array. The callback function is not executed for the first value.
- When you want the callback function to execute for every value in the array and you want the reduce function to start with a specific value: use the optianal initial value of the reduce. 
- Use index when you need different calculations for some values in the array

Bonus 1:  Figure out why the first example doesnt need an initial value. <br>
Bonus 2:  Try it yourself. I already gave some examples in the codepen which you can alter. 

{% codepen https://codepen.io/RhodeZ/pen/wvwVddP default-tab=js %}


