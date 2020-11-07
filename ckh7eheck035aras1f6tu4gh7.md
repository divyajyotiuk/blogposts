## Easy peasy First Odd Int

In a given array, find the first integer that appears an odd number of times. Given that **only one** integer occurs odd number of times.

One line solution to this is by using the infamous reduce operation of Javascript. 

```javascript
const findOddInt = (arr) => arr.reduce((a, b) => a ^ b);
```
Always go for functional and tuned solution, reason it being faster ;)

For those who are wondering, **^** is the symbol for XOR. `a^a = 0` and `0^a = a`. So, all the numbers that occur even times will get reduced to 0 and the number that occurs odd number of times would remain. 