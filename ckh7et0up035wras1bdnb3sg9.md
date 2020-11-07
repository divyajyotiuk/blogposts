## Easy peasy reverse words

Return string with **`n` or more lettered** words reversed, given that string consists of letters and spaces only. (i.e. n is the word length) 

A single line clever solution would be by using `regex`.
If `n` is predetermined, like `n = 5`, 
```js
const revWords = (str) => {
  return str.replace(/\w{5,}/g, function(w) { 
    return w.split('').reverse().join(''); });
}
```

But not all clever solutions are good to go on production. It does fit this problem but difficult to mutate or reuse the technique if problem changes. The next one's better.

```js
const revWords = (str, n) => {
  return str.split(' ').map(function (word) {
    return (word.length >= n) ? 
    word.split('').reverse().join('') : word;
  }).join(' ');
}
```