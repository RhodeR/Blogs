## The basics
You probably have once read about the reduce function, when you saw the syntax of reduce: 'arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])'. A tear came out of your eye. Don't worry; you are not the only one, who did not understand this immediately. The good news: it's way easier than it looks. It's just a simple for loop with some syntactic sugar to make your life easier. So take a look at the for loop underneath; A loop over every value of the array. Where each value of the array is saved in the variable 'memory'.


```javascript
const myArray = [2,3,4,5,6]
let memory=0;

for (let i = 0; i<myArray.length; i++ ) {
memory = memory + myArray[i] 
}

console.log(memory) // => 20 
```

The reduce function underneath does exactly the same as the former for loop, only in one line! 
The memory (accumulator) variable in the reduce function has the same 

```javascript
const myArray = [2,3,4,5,6]

let reduced=myArray.reduce((memory, arrayVal) => { arrayVal > memory ? arrayVal : memory });

console.log(reduced); // => 20
```

## Why and how to use index 
Sometimes you want to execute different calculations for each value in the array. 
For example: you want to multiply each of your arrayValues with the index of the arrayValue. 
In the classic for loops there was an i variable, which enabled you to do the this: myArray[i]. 
To solve this issue with the reduce function there is an optianal index value, which you are able to use as shown below. 

```javascript
const myArray = [2,3,4]
let reduced=myArray.reduce((memory, arrayVal, i) => memory + (arrayVal * i));

 console.log(reduced); // => 13
```

What? What happened? The mathematicians noticed immedeately: 'This isn't right'. It's not what you expected:  (2 * 0) + (3 * 1) + (4 * 2) = 11! Not 13... Let's approach this issue in a professional way, console log ;). 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((memory, arrayVal, i) => 
                    {console.log('memory=' + memory + ' arrayVal=' + arrayVal + ' i=' + i); 
                     return memory + arrayVal * i
                     }); 

console.log('reduced=' + reduced); 

                      // => memory=2   arrayVal=3   i=1, 
                      // => memory=5   arrayVal=4   i=2
                      // => reduced=13
```

## InitialValue to the rescue
You would expect that the calculation would start that the first iteration started with a memory and i value of 0 en arrayVal of 2, but that's not how it works. The callback function is invoked two times; for index 1 and index 2. Not for index 0. But it still uses the value on index 0, by putting it in it's memory variable. So in the example above it starts with the memory value of 2. Okay.. cool. Only the thing is: I don't want it to start with the value 0f 2.. I want to start with the value of zero. How to fix this?

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((memory, arrayVal, i) => memory + arrayVal * i, 0); 

console.log('reduced=' + reduced); 

                      // => memory=0   arrayVal=2   i=0
                      // => memory=2   arrayVal=3   i=1, 
                      // => memory=5   arrayVal=4   i=2
                      // => reduced=13
```

See what is changed? In the code above I added a 0 after the callback function. Now the callback function is invoked three times as you would expect. 

So when do you need an initialValue?
-
-
-







