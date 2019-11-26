# Console Debugging in Chrome

## Display objects as a table
Sometimes, you have a complex set of objects that you want to view. You can either console.log them and scroll through the list, or break out the console.table helper. Makes it easier to see what you’re dealing with!

```js
var animals = [
    { animal: 'Horse', name: 'Henry', age: 43 },
    { animal: 'Dog', name: 'Fred', age: 13 },
    { animal: 'Cat', name: 'Frodo', age: 18 }
];
 
console.table(animals);
```

Will output:
![](https://djenjyj46f9j9.cloudfront.net/items/1q433a2W1B101Q1q3L1u/Image%202019-11-26%20at%208.30.45%20AM.png?X-CloudApp-Visitor-Id=3221729)
