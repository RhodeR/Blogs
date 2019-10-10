## The basics
You probably have once read about the reduce function, when you saw the syntax of reduce:

**'arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])'.**

 A tear came out of your eye, after which you needed alcohol.. a lot of it. Don't worry; you are not the only one who did not understand this immediately. The good news: it's way easier than it looks. With the reduce function in the snippet underneath you can get the same thing done as in a for loop snippet underneath, only in one line! The 'myArray[i]' variable in the for loop is comparable with the 'arrayVal' of the reduce function. The count variable in the for loop is comparable with the count variable in the reduce function, it's that easy. Unfortunately, the word abstract and freightening word 'accumulator' is chosen in the syntax of the reduce. 


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
//count= 20
```

The result of count is the same, but when you take a closer look you'll see that under the hood there is a slight difference. The reduce functions initial value of the count/accumulator variable is the value in myArray[0]. The callback function is not executed for myArray[0], you'll see that when you put a console.log in the callback function; arrayVal 2 is never logged. In this example it will give the right/expected outcome because we are adding up. But there are lots of examples where this could be confusing. Take a look at the snippet underneath. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((count, arrayVal, i) => count + arrayVal * 3); 
 // => count=2   arrayVal=3, 
 // => count=5   arrayVal=4,
 // => reduced=23
```

What? What happened? The mathematicians noticed immedeately: 'This isn't right'. It's not what you expected:  (2 * 3) + (3 * 3) + (4 * 3) = 27. Not 23... In need of more alcohol...! Here you see very clearly that the callback function isn't executed for the fist value in the array, it only takes that value as the initial value, which gives the sum of 2 + 3*2 + 4*2 




## Why and how to use index 
Sometimes you want to execute different calculations for each value in the array. 
For example: you want to multiply each of your arrayValues with the index of the arrayValue. 
In the classic for loops there was an i variable, which enabled you to do the this: myArray[i]. 
To solve this issue with the reduce function there is an optianal index value, which you are able to use as shown below. 

```javascript
const myArray = [2,3,4]
let reduced=myArray.reduce((memory, arrayVal, i) => memory + (arrayVal * i));
// => reduced=13
```



## InitialValue to the rescue
You would expect that the calculation would start that the first iteration started with a memory and i value of 0 en arrayVal of 2, but that's not how it works. The callback function is invoked two times; for index 1 and index 2. Not for index 0. But it still uses the value on index 0, by putting it in it's memory variable. So in the example above it starts with the memory value of 2. Okay.. cool. Only the thing is: I don't want it to start with the value 0f 2.. I want to start with the value of zero. How to fix this?

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((memory, arrayVal, i) => memory + arrayVal * i, 0); 


                      // => memory=0   arrayVal=2   i=0
                      // => memory=2   arrayVal=3   i=1, 
                      // => memory=5   arrayVal=4   i=2
                      // => reduced=13
```

See what is changed? In the code above I added a 0 after the callback function. Now the callback function is invoked three times as you would expect. 

Summary
-
-
-







