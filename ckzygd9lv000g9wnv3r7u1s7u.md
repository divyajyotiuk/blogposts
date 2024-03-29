## Subset/Subsequence Pattern

### Subset

Subset patterns deal with Permutation and Combinations.

e.g.

```javascript
"abc" -> [ "abc", "acb", "bac", "bca", "cab", "cba" ] //permutations
[1,2,3] -> [ [],[1], [2], [3], [1,2], [2,3], [1,3], [1,2,3] ]
```

We can solve permutations with the help of subset pattern

Time Complexity - **O(n!)**

```javascript
let arr = [];
function permutations(processedStr='',unprocessedStr=''){

    if(unprocessedStr.length == 0){ // string processed
        arr.push(processedStr);
        return;
    }

    // recursion calls increase with increase in processed string length
    for(let i=0;i<=processedStr.length;i++){ 
        // processedStr = "a" ; unprocessedStr = "bc"
        // newString = ""(0,0) + "b" + "a"(0,1)
        // newString = "a"(0,1) + "b" + ""(1,1)
        let newString = processedStr.slice(0,i) + unprocessedStr[0] + processedStr.slice(i,processedStr.length);
        permutations(newString, unprocessedStr.substring(1));
    }

}

permutations("","abc");
console.log(arr); // [ "abc", "acb", "bac", "bca", "cab", "cba" ]
```

Wherever you see a question that tells you to take some elements and remove some elements, that is your subset pattern problem

Iterative approach 

```javascript
function iterativeSubset(unprocessedArr=[]){
    let processedArr = [];

    // start with empty array
    if(unprocessedArr.length > 0){
        processedArr.push([]) // push empty array
    }

    for(let i=0;i<unprocessedArr.length;i++){ // for every pass #subsets gets doubled
        let copyOfProcessed = [...processedArr];
        for(let j=0;j<copyOfProcessed.length;j++){
            copyOfProcessed[j] = copyOfProcessed[j].concat([unprocessedArr[i]]);
        }
        processedArr = processedArr.concat(copyOfProcessed);
    }

    return processedArr;
}

ans = iterativeSubset([1,2,3]);
console.log(ans); // [[],[1], [2], [3], [1,2], [2,3], [1,3], [1,2,3]]
```

### Subsequence

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

### Complexity Analysis

Time complexity - **O(n*2^n)** 
<br>`n` -> number of elements
<br>`2^n` -> no of subsets for n elements

Space complexity - **O(n*2^n)** 
<br>`n` -> space taken by the subset
<br>`2^n` -> number of subsets

