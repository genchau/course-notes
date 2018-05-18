## Scrimba - Introduction to ES6+ 
##### Lessons 1 to 23. Date started: 05/16/2018. [Link to course](https://scrimba.com/g/gintrotoes6) 
- - -   
### Lesson 1 Introduction
- Core ES6+ features.
-  17 lessons. 
-  4 challenges.
Instructor: Dylan Israel, Front-end engineer & online instructor.
- - -
### Lesson 2 Template Literals

Old style of concatenating strings:
```
let word1 = 'Dylan';
let word2 = 'Israel';

const fullName = word1 + ' ' + word2;

console.log(fullName);
```

template literals:
```
let word1 = 'Dylan';
let word2 = 'Israel';

const fullName = `${word1} ${word2}`;

console.log(fullName);
```

old way, you need `\n` to start new line:
```
let example = 'Hello \n' + 'world';
document.getElementById('example').innerText = example;
```
new way:
```
let example = `${word1}
${word2}
`;
```
- - -
### Lesson 3 Destructuring Objects

assigning variables object's properties is simpler and more intuitive: `fn` and `ln` are variables being assigned a value from the object personalInformation:
```
const personalInformation = {
    firstName: 'Dylan',
    lastName: 'Israel',
    city: 'Austin',
    state: 'Texas',
    zipCode: 73301
};

const {firstName: fn, lastName: ln} = personalInformation;

console.log(`${fn} ${ln}`);
```
- - - 
### Lesson 4 Destructuring Arrays

```
let [firstName, middleName, lastName] = ['Dylan', 'Coding God', 'Israel'];

console.log(firstName + middleName)
```
- - -
### Lesson 5 Object Literal

old:
```
function addressMaker(city, state) {
    const newAdress = {newCity: city, newState: state};
    
    console.log(newAdress);
}

addressMaker('Austin', 'Texas');
```

new:
```
function addressMaker(city, state) {
    const newAdress = {city, state};
    
    console.log(newAdress);
}

addressMaker('Austin', 'Texas');
```
- - -
### Lesson 6 Object Literal (Challenge)

Challenge start:
```
function addressMaker(address) {
    const newAddress = {
        city: address.city,
        state: address.state,
        country: 'United States'
    };
    
}

addressMaker({city: 'Austin', state: 'Texas'});
```
Solution:
```
function addressMaker(address) {
    const {city, state} = address;
    
    const newAddress = {
        city,
        state,
        country: 'United States'
    };
    console.log(`${newAddress.city}, ${newAddress.state}, ${newAddress.country}`)
}

addressMaker({city: 'Austin', state: 'Texas'});
```
- - -
### Lesson 7 For of Loop

We can iterate over arrays, strings with the for of loop:
```
let fullName = "Dylan Coding God Israel";

for (const char of fullName) {
    console.log(char);
}
```
- - -
### Lesson 8 For of Loop (Challenge)
skip
- - -
### Lesson 9 Spread Operator

The spread ... operator basically makes a duplicate of an array or object. It's not just a reference to the same array or object, but a 2nd copy.
```
let example1 = [1,2,3,4,5,6];
let example2 = [...example1];
```
- - -
### Lesson 10 Rest Operator

here's how to use the rest operator:
```
function add(...nums) {   
    console.log(nums);
}
add(4, 5, 7, 8, 12)
```
output: `[4, 5, 7, 8, 12]`
- - -
### Lesson 11 Arrow Functions

Arrow functions basically replaces the old function layout:
```
function add(...nums) {
    let total = nums.reduce( (accumulator, currentValue) => accumulator + currentValue );   
    console.log(total);
}
add(4, 5, 7, 8, 12)
```
- - -
### Lesson 12 Default Params

Default parameters can be setup for functions, so in the case of incorrect input, the function won't error, but return in this case a value of 0.
```
function add(numArray = []) {
    let total = 0;
    numArray.forEach((element) => {
        total += element;
    });   
    console.log(total);
}
add();
```
- - -
### Lesson 13 includes()

includes() is a new function to let us know if an array contains the value, returning true or false. The old way to check was using indexOf() but it did not return true/false.
```
let numArray = [1,2,3,4,5];
console.log(numArray.includes(2))
```
- - -
### Lesson 14 Let & Const

let and const was created to replace var. Due to hoisting var will be created by assigned null. But in reality if it's in an if statement that doesn't get executed, the variable shouldn't exist. So with let and const they are block variables and will only exist when inside the block.
- - -
### Lesson 15 Import & Export

example.js:
```
export const data = [1,2,3];
```
index.js:
```
import { data } from './example.js';
let updatedData = data;
updatedData.push(5)
console.log(updatedData);
```
- - -
### Lesson 16 padStart() & padEnd()

Interesting feature. So the function takes 2 parameters. The first one being the total string length. And then the second is the string you want to fill it with.

```
let example = 'Dylan';
console.log(example.padEnd(10, 'a'));
```
output: `Dylanaaaaa`
- - -
### Lesson 17 padStart() & padEnd() (Challenge)

The second parameter is optional. It'll add empty characters. The length is 100, but you won't see the empty characters.
- - -
### Lesson 18 Classes

animal.js
```
export class Animal {
    constructor(type, legs) {
        this.type = type;
        this.legs = legs;
    }
    
    makeNoise(sound = 'Loud Noise') {
        console.log(sound);
    }
    
    get metaData() {
        return `Type: ${this.type}, Legs: ${this.legs}`;
    }
    
    static return10() {
        return 10;
    }
}

export class Cat extends Animal {
    makeNoise(sound = "meow") {
        console.log(sound);
    }
}
```
index.js
```
import { Animal, Cat } from './animal.js';

let cat = new Cat('Cat', 4);

cat.makeNoise();

console.log(cat.metaData)
```
- - - 
### Lesson 19 Trailing Commas

a trailing comma will not create an error.
```
function add(param1,){
    const example = {
        name: 'Dylan',
    };
    
    console.log(example)
};

add(2);
```
- - -
### Lesson 20 Async & Await

Async can have an await expression, which pauses the execution of the async function.
```
const apiUrl = 'https://fcctop100.herokuapp.com/api/fccusers/top/alltime';

async function getTop100Campers() {
    const response = await fetch(apiUrl);
    const json = await response.json();
    
    console.log(json[0]);
}

// function getTop100Campers() {
//     fetch(apiUrl)
//     .then((r) => r.json())
//     .then((json) => {
//         console.log(json[0])
//     }).catch((error) =>{
//         console.log('failed');
//     });
// }

getTop100Campers();
```
- - -
### Lesson 21 Async & Await (Challenge)

```
function resolveAfter3Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 3000);
  });
}

// resolveAfter3Seconds().then((data) => {
//     console.log(data);
// });

async function getAsyncData() {
    const result = await resolveAfter3Seconds();
    console.log(result);
}

getAsyncData();
```
result: `resolved`
- - -
### Lesson 22 Sets

```
const exampleSet = new Set([1,1,1,1,2,2,2,2]);

exampleSet.add(5);
exampleSet.add(5).add(17);

console.log(exampleSet.has(5));

exampleSet.clear();

console.log(exampleSet.size);
```
- - -
### Lesson 23 What's Next

- - -
Return to [Table of Contents](TableOfContents.md)
