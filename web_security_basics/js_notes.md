# __essential Javascript notes__ 🗒️📝


## __Loops in JS__
### __For Loop:-__

```javascript 
for (let i = 1; i <= 5; i++) {

console.log("apna college");
}
```
## __while loop__ :-

```javascript 
let val = 5;
while (val < 5){
    console.log(val);
    val ++
}
```
## __do-while loop__ :-
- it will do some work for one time without checking. then it will check the condition.

```javascript 
do {
    console.log("hello everyone");
}while(1 = 0);

//output 
hello everyone.
```

## __for-of loop__ :-
- Can be applied on array's & string;

```js
let str = "Deepika yadav";
let size = 0;
for (let char of str) {
    console.log("char",char);
    size++
}

console.log(size);

//output  on seperate lines
D e e p i k a y a d a v
```
## __for-in loop__ :-

- for object's and array;
- in object's used to get key's from key-value pair.

```js
let student = {
    name: "Deepika yadva",
    age: 15,
    isPass: true,
}

for (let key in student){
    console.log("key=",key,"value=",student[key]);
}

//output 
key= name value= Deepika yadav ....
```
## __Practice__ :-
Q1 - Print all even numbers from 0 to 100.?

```js 
for (let i = 0; i<= 100; i++) {
    console.log(i);
}
```

Q2 - Create a game where you start with any random game number. Ask the user to keep
guessing the game number until the user enters correct value.

```js
let random_num = "5";
let user_num = prompt("Enter a number");
let bool = false;
console.log(typeof user_num);
console.log(typeof random_num);

do {
    if (random_num !== user_num) {
    user_num = prompt("Enter a number");
    bool = false;
}else {
    alert("Congrat's it's correct",user_num);
    bool = true;
}
}while(bool !== true);
```
## String's in JS
- String is a sequence of characters used to represent text

- `Create String` :-
  +  let str = “Apna College“;

- `String Length`
  + str.length

- `'String Indices'`
  + str[0], str[1], str[2]


## __Template literal in string__ :-

A way to have embedded expressions in strings:-

`string text ${expression} string text`

## __String Methods in JS__ :-
- str.toUpperCase( )

- str.toLowerCase( )

- str.trim( ) // removes whitespaces

## __String Methods in JS__ :-
