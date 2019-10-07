## Header 2
You probably have once read about the reduce function, when you saw the syntax of reduce: 'arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])'. 
A tear came out of your eye. Don't worry; you are not the only one, who did not understand this immediately. 

The good news: it's way easier than it looks. It's just a simple for loop with some syntactic sugar to make your life easier.

So take a look at the for loop underneath; A loop over every value of the array. 
Where each value of the array is saved in the variable 'memory'.


```javascript
const myArray = [2,3,4,5,6]
let memory=0;

for (let i = 0; i<myArray.length; i++ ) {
memory = memory + myArray[i] 
}

console.log(memory) // => 20 
```

The reduce function underneath does exactly the same as the former for loop, only in one line! 
The memory variable in the reduce function has the same 

```javascript
const myArray = [2,3,4,5,6]

let reduced=myArray.reduce((memory, arrayVal) => { arrayVal > memory ? arrayVal : memory });

console.log(reduced); // => 20
```
Sometimes you want to execute different calculations for each value in the array. 
For example: you want to multiply each of your arrayValues with the index of the arrayValue. 
In the classic for loops there was an i variable, which enabled you to do the this: myArray[i]. 
To solve this issue with the reduce function there is an optianal index value, which you are able to use as shown below. 

```javascript
const myArray = [2,3,4]
let reduced=myArray.reduce((memory, arrayVal, i) => memory + (arrayVal * i));

 console.log(reduced); // => 13
```

What? What happened. Not cool. The mathematicians noticed immedeately: 'This isn't right'. It's not what you expected:  (2 * 0) + (3 * 1) + (4 * 2) = 11! Not 13... What happened? 
Let's approach this issue in a professional manner, which is console log everywhere.
When you put a console. 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((memory, arrayVal, i) => 
                    {console.log('memory=' + memory + ' arrayVal=' + arrayVal + ' i=' + i); 
                     return memory + arrayVal * i
                     }); 

console.log('reduced=' + reduced); 

                      // => memory=2 arrayVal=3 i=1, 
                      // => memory=5 arrayVal=4 i=2
                      // => reduced=13
```

You would expect that the calculation would start with 0*2, cause the memory value is 0, arrayVal is 2, and i=0. 
But that is not how it works. The first index is 1, and the first memory value also. So it starts with the value 2



Extra: Try it yourself in codepen: 

```javascript
const myArray = [2,3,4]
let reduced= myArray.reduce((memory, arrayVal, i) => { console.log('memory=' + memory + ' arrayVal=' + arrayVal + ' i=' + i); 
return memory + arrayVal * i}); 
console.log(reduced);
```