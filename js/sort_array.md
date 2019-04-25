# JavaScript
```JS
var items = [
  { name: 'Edward', value: 21, score:10 },
  { name: 'Sharpe', value: 37, score:3 },
  { name: 'And', value: 45, score:1 },
  { name: 'The', value: -12, score:6 },
  { name: 'Magnetic', score:1 },
  { name: 'Zeros', value: 37, score:5 }
];
items.sort(function (a, b) {
  if (a.name > b.name) {
    return 1;
  }
  if (a.name < b.name) {
    return -1;
  }
  // a must be equal to b
  return 0;
});
console.log(items);
```
