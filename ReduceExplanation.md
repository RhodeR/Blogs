## Header 2
You probably have once read about the reduce function, when you saw the syntax of reduce: 'arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])'. 
A tear came out of your eye. Don't worry; you are not the only one. 

The good news: it's easier than it looks. It's just a simple for loop with some syntactic sugar to make your life easier.

So take a look at the for loop underneath; A loop over every value of the array. 
Where each value of the array is saved in the variable 'memory'.
The reduce function underneath the forloop does exactly the same, only in one line! 
The memory variable in the reduce function has the same 

```javascript
const myArray = [2,3,4,5,6]
let memory=0;

for (let i = 0; i<myArray.length; i++ ) {
memory = memory + myArray[i] 
}
console.log(memory) // => 


const myArray = [2,3,4,5,6]
let reduced=myArray.reduce((memory, arrayVal) => { arrayVal > memory ? arrayVal : memory });
console.log(reduced); // => 15
```
Sometime    s you want to do different calculations for each value in the array. Therefore you can include the index in your reduce function. 
For example: you want to multiply each of your arrayValue with the index of the arrayValue. 

const myArray = [2,3,4,5,6]
let reduced=myArray.reduce((memory, arrayVal, i) =>  memory = memory + arrayVal * i);
 console.log(reduced);

You would expect that the calculation would start with 0*2, cause the memory value is 0, arrayVal is 2, and i=0. 
But that is not how it works. The first index is 1, and the first memory value also. So it starts with the value 2