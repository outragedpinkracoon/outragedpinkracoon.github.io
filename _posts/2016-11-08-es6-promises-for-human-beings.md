---
title: ES6 Promises for Human Beings
description: An easier to digest explanation of how promises work in ES6.
layout: post
categories: [javascript, programming]
---
I was really struggling to find some easy to digest explanations of promises so I've shared an example here that I wish I had found when I was searching.

## THE PROBLEM
Callbacks get us into this sort of v-shaped spaghetti situation, where we have lots of dependent things nested inside of each other. Have a look at this Node code:

```javascript
var fs = require('fs');

const readFile = function(fileName,callback){
  fs.readFile(fileName, (err, data) => {
    if(err) return err;
    callback(data.toString());
  });
}
```
It wraps around the fs.readFile method to allow us to invoke a callback when a file has finished being read. So let’s image we want to read a file called 1.txt and output it’s content to the screen.

```javascript
readFile('1.txt',function(data){
  console.log(data);
});
```
Grand. What if we want to read 2 files in order, 1.txt then 2.txt and concat the contents and output it to the screen?

```javascript
readFile('1.txt', (data) => {
  var result = data;
  readFile('2.txt',(data) => {
    result += data;
    console.log(data);
  });
});
```
You can already see a bit of nesting happening but it’s not too bad.

But what if we want to read 6 files in order?

```javascript
readFile('1.txt', (data) => {
  let result = data;
  readFile('2.txt', (data) => {
    result += data;
    readFile('3.txt', (data) => {
      result += data;
      readFile('4.txt', (data) => {
        result += data;
        readFile('5.txt', (data) => {
          result += data;
          readFile('6.txt', (data) => {
            result += data;
            console.log(result);
          });
        });
      });
    });
  })
})
```
![that escalated quickly](/assets/images/es6-promises-1.jpg)

You can see the v-shaped situation we have gotten ourselves into, because we need our callbacks to be invoked for the next step of the chain to happen. This isn’t great because it’s damned hard to follow and quickly becomes a mess - especially if there is complex code happening in each step of the callback chain.

## PROMISES TO THE RESCUE
Luckily there is a better way. The concept of a promise is not new - they were available before from libraries such as bluebirdjs. However they are now available straight of the box in ES6 which is great news.

Promises allow us to define what happens when an event is either successful or unsuccessful and invoke chains of events we want to happen in sequence. This is exactly what we need to sort out the mess you can see above.

We need to make a modification to our file reading function. From the function we want to be dependant on, we are going to return a Promise object which gives us access to methods that are going to make our lives easier - more on this in a bit. This is going to look really weird but bare with me.

```javascript
const readFile = (fileName, result) => {   //UPDATED
  return new Promise((resolve, reject) => { //NEW
    fs.readFile(fileName, (err, data) => {
      if(err) return reject(err); //UPDATED
      resolve(result + data.toString()); //UPDATED
    })
  });
}
```
Note the `resolve` and `reject` functions that the promise passes in for us to use in the callback. We can control what happens when the promise is successful and when the promise is unsuccessful. In this case, if we get an error (err) then we want to invoke reject and pass the error. If not, we want to invoke resolve and pass the concatenated result.

Notice also that we are passing in the result now to our function so that we can chain it together and keep track of it. There is no need to pass in a callback anymore.

Cool. Keep breathing. It’ll all make sense in a second.

We haven’t actually used the code yet, it’s just sitting there bundled up in a promise ready to go. The next step is to actually call it.

We can completely remove the v-shaped nightmare we created and replace it with chained calls to our function above, using the Promise object.

```javascript
readFile('1.txt', "") //first call to the function
  .then((result) => readFile('2.txt', result)) //call has completed successfully
  .then((result) => readFile('3.txt', result))
  .then((result) => readFile('4.txt', result))
  .then((result) => readFile('5.txt', result))
  .then((result) => readFile('6.txt', result))
  .then((result) => console.log(result))
  .catch((err) => console.log("error: ", err.message)); //there has been an error
```
The first big difference is here is there is no v-shaped spaghetti junction. It’s nice and linear and we can read exactly what is going on. Notice that .then() contains result, which we pass into the resolve function. Our resolve action maps directly to the then() method here, allowing us to consume the result and if we like chain this onto something else. This is only possible by returning a Promise object!

Notice also the .catch() method at the end of the chain. The “reject” function call from earlier directly maps to this - you can see the “err” object from earlier making an appearance. If any of the promises in the chain fail, this will be invoked.

Pretty neat huh??

## PROMISE.ALL
One of my favourite things about promises is that we can use `Promise.all` to fire off a whole bunch of stuff at once, and rely on Promises to gather up all the results and tell us when all the events have completed. This is basically a nightmare to do otherwise.

Sticking to our little file reading example, we can fire off all the file reading events at once harnessing the power of JavaScripts async nature.

Our little readFile function remains the same, but the way we fire off our function changes.

First, we need to put our promises into an array. The easiest way to do this is using a map:

```javascript
const fileNames = ["1.txt", "2.txt", "3.txt"] //NEW
const promises = fileNames.map(readFile); //NEW
```
`Promise.all` requires one argument, which is an array of promises. It will fire them all off and collect the results for us! More than that, the results will be presented back to us in the order we fired them off. Whaaat! This is crazy stuff right here.

In this example I’m going to add all the results together.

```javascript
Promise.all(promises)  //NEW
  .then((results) => { //collect all the results and give me them
    let data = 0; //I can decide what to do here
    results.forEach((item) => {
      data += parseInt(item);
    });
    console.log("Result was: ", data);
  })
  .catch((err) => { //one of the promises has failed
    console.log("Failed:", err);
  });
```
All of the promises in the array must succeed for then() to be invoked, otherwise the catch() branch will fire. This is AMAZING! Isn’t it?? Come on. You have to be excited right now.
