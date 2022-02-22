## Subset/Subsequence Pattern

Subset patterns deal with Permutation and Combinations.

e.g.

```
[1,2,3] -> [[1], [2], [3], [1,2], [2,3], [1,3], [1,2,3]]
```

Wherever you see a question that tells you to take some elements and remove some elements, that is your subset pattern problem

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters

Let's look at subsequence of string - 

```
"abc" -> "a", "b", "c", "ab", "bc", "ac", "abc"
```

The recursion call can be visualised as follows:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645549847082/ytXC9T9_p.png)

We take processed string, unprocessed string and the array that is to be returned as arguments for our recursion call.

```javascript
function subsequence(processedStr, unprocessedStr, arr=[]){
    
    if(unprocessedStr.length == 0){
        return;
    }

    // include the unprocessedStr[0] in processedStr
    // move ahead
    subsequence(processedStr + unprocessedStr[0],unprocessedStr.substring(1),arr);
    arr.push(processedStr + unprocessedStr[0]);

    // ignore the unprocessedStr[0], send processedStr as is forward
    subsequence(processedStr,unprocessedStr.substring(1),arr);

    return arr;
}

ans = subsequence("","abc");
console.log(ans);

```
