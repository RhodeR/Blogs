## The basics
You probably have once read the reduce function on MDN, with the following syntax:

**'arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])'.**

 A tear came out of your eye, and you were in need of alcohol.. a lot of it. Don't worry; you are not the only one who did not understand this immediately. The good news: it's way easier than it looks. With the reduce function you can get the same thing done as with the good old for loop, only in one line! Take a look at the for loop and the reduce function in the snippets underneath. The 'myArray[i]' variable in the for loop is comparable with the 'arrayVal' of the reduce function. The count variable in the for loop is comparable with the count variable in the reduce function, it's that easy. In the code examples below I renamed the variable 'accumulator', which is used in de MDN syntax of reduce, to 'count', cause 'accumulator' is a terrible abstract word. With 'count' it's easier to understand what's happening and you can see the simularity with the for loop. 


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

The results of both snippets are the same, but when you take a closer look you'll see that there are some differences. The initial value of the count/accumulator variable of the reduce function is the value in myArray[0]. The callback function is not executed for myArray[0], you'll see that when you put a console.log in the callback function. ArrayVal 2 is never logged. However in this example above the reduced funtion will give the right/expected outcome because we are adding the arrayVal on the count val. However there are lots of examples this is not the case. Take a look at the snippet underneath. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((count, arrayVal) => count + arrayVal * 3); 

 // => count=2   arrayVal=3, 
 // => count=5   arrayVal=4,
 // => reduced=23
```

What? What happened? The mathematicians noticed immedeately: 'This isn't right'. When you take a look at the callback function this is what you expected:  (2 * 3) + (3 * 3) + (4 * 3) = 27. But the outcome is 23... I want more alcohol... Here you see very clearly that the callback function isn't executed for the fist value in the array, as I said earlier, it only takes that first arrayValue as the initial value, thereby the calculation is: 2 + (3 * 3)  + (4 * 3). 

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

See what is changed? In the code above I added a 0 after the callback function. Now the callback function is invoked three times as you would expect. <br>
0 + 3 * 2 =6 <br>
6 + 3 * 3 = 15 <br> 
15 + 4 * 3= 27 

## Why and how to use index 
One more important issue to address. Sometimes you want to execute different calculations for each value in the array. 
For example: you want to multiply each of your arrayValues with the index of the arrayValue. In the classic for loops you were able to do this by: myArray[i]. In the reduce function you are able to use the optianal index value, which can be used as shown in the snippet below. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((count, arrayVal, i) => count + arrayVal * i, 0); 


// => count=0   arrayVal=2   i=0
// => count=2   arrayVal=3   i=1, 
// => count=5   arrayVal=4   i=2
// => reduced=13
```

Summary
- Reduce is easy to understand, do'nt be scared by the syntax. 
- The initial value of the reduce function is the first value of the array. The callback function is not executed for the first value.
- When you want the callback function to execute for every value in the array and you want the reduce function to start with a specific value: use the initial value of the reduce. 
- Use index when you need different calculations for some values in the array


When to use reduce?







