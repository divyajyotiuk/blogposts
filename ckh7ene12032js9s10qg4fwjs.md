## Easy peasy split the string

The question is to split string in such a way that each element in the array has two characters and if the length of the string is odd then the missing character should get replaced by '_'.


Example: 

`input: "abc"`

`output: ["ab", "c_"]`


`input: "abcd"`

`output: ["ab", "cd"]`


So the single line solution is: 

```javascript
const splitString2 = (str) => str.concat('_').match(/../g);
```

`String.prototype.match()` takes parameters as regular expressions object and returns an array whose value depends on presence and absence of `g` flag. The `g` flag returns all results matching the `regex`.


The dot(.) in regex represents any character except newline. Therefore, `/../g` represents two characters to match.  

Happy coding!
