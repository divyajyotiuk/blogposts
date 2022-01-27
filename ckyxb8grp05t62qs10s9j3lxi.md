## Binary Search

### Code

Given a **sorted** array, perform binary search.

Time Complexity - **O(log n)**

```javascript
function binarySearch(sarr=[], term, i, j){
    if(!sarr.length) return -1;
    let k = Math.floor((i+j)/2);
    if(sarr[k] == term) return k;
    if(term > sarr[k]) return binarySearch(sarr, term, k, j);
    if(term < sarr[k]) return binarySearch(sarr, term, i, k);
    return -1;
}
```
