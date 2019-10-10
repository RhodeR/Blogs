## The basics
You probably have once read the reduce function on MDN, with the following syntax:

**'arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])'.**

 A tear came out of your eye, and you were in need of alcohol.. lots of it. Don't worry; you are not the only one who did not understand this immediately. The good news: it's way easier than it looks. With the reduce function you can get the same thing done as with the good old for loop, only in one line! Take a look at the for loop and the reduce function in the snippet underneath. The 'myArray[i]' variable in the for loop is comparable with the 'arrayVal' of the reduce function. The count variable in the for loop is comparable with the count variable in the reduce function, it's that easy. In the code examples below I renamed the variable 'accumulator', which is used in de MDN syntax of reduce, to 'count', cause in that way it's a lot easier to understand what is happening in the snippets below and to see the simularity with the for loop. 


```javascript
const myArray = [2,3,4,5,6]
let count=0;

for (let i = 0; i<myArray.length; i++ ) {
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

The result of count in both the snippets is the same, but when you take a closer look you'll see that  there is a slight difference under the hood. The initial value of the count/accumulator variable of the reduce function is the value in myArray[0]. The callback function is not executed for myArray[0], you'll see that when you put a console.log in the callback function. ArrayVal 2 is never logged. However in this example the reduced funtion will give the right/expected outcome because we are adding the arrayVal on the count val. But there are lots of examples where the result is not what you expected. Take a look at the snippet underneath. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((count, arrayVal) => count + arrayVal * 3); 
 // => count=2   arrayVal=3, 
 // => count=5   arrayVal=4,
 // => reduced=23
```

What? What happened? The real mathematicians noticed immedeately: 'This isn't right'. When you take a look at the callback function this is what you expected:  (2 * 3) + (3 * 3) + (4 * 3) = 27. But the outcome is 23... I want more alcohol... Here you see very clearly that the callback function isn't executed for the fist value in the array, it only takes that first arrayValue as the initial value, which brings ut at the following calculation: 2 + (3 * 3)  + (4 * 3). 

Okay.. fine, when I really have to accept that for the first arrayValue the callback function is not executed, I will accept it. But sometimes you want the callback function to be executed for **every** value in the array. 

## InitialValue to the rescue
In that case you are able to use the initialValue of the reduce function, as is shown in the snippet below. 

____________________________________________________FixMe!!!!!!! variables are not right. Names and values. ________________________________________________________

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((memory, arrayVal) => memory + arrayVal * 3, 0); 


                      // => memory=0   arrayVal=2   i=0
                      // => memory=2   arrayVal=3   i=1, 
                      // => memory=5   arrayVal=4   i=2
                      // => reduced=13
```

See what is changed? In the code above I added a 0 after the callback function. Now the callback function is invoked three times as you would expect. 

## Why and how to use index 
One more issue is left; sometimes you want to execute different calculations for each value in the array. 
For example: you want to multiply each of your arrayValues with the index of the arrayValue. 
In the classic for loops there was an i variable, which enabled you to do the this: myArray[i]. 
To solve this issue with the reduce function there is an optianal index value, which can be used as shown in the snippet below. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((memory, arrayVal, i) => memory + arrayVal * i, 0); 


// => memory=0   arrayVal=2   i=0
// => memory=2   arrayVal=3   i=1, 
// => memory=5   arrayVal=4   i=2
// => reduced=13
```

Summary
-
-
-







