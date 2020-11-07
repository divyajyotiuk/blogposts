## Easy peasy formatting list

Given an array containing hashes of names.
You have to return a string formatted as a list of names separated by commas except for the last two names, which should be separated by `&`.

```
formatList([ {name: 'Dave'}, {name: 'Alex'}, {name: 'Marge'} ])
// returns 'Dave, Alex & Marge'
```
Here's a single line solution, `regex` peeps
```js
let formatList = (names) => names.map(x => x.name).join(', ').replace(/(.*),(.*)$/, "$1 &$2");
```

But this is the most clever solution, I could never think of:
```js
let formatList = (names) => {
  let a = names.map(obj => obj.name);
  let name = a.pop();
  return a.length ? a.join(", ") + " & " + name : name || "";
}
```
I could think of using `reduce`, `forEach` and other looping methods using if else. `reduce` does a pretty great job itself.
```js
let formatList = (names) => {
  return names.reduce((prev, curr, i, arr) => {
    return prev + curr.name + (i < arr.length - 2 ? ', ' : i == arr.length - 2 ? ' & ' : '');
  }, '');
}
```
