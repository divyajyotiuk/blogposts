## Binary Search

Given a **sorted** array, perform binary search.

Time Complexity - **O(log n)**


```javascript
function binarySearch(sarr=[], target, start, end){
    if(!sarr.length) return -1;
    let middle = Math.floor((start+end)/2);
    if(sarr[middle] == target) return middle;
    if(target > sarr[middle]) return binarySearch(sarr, target, middle, end);
    if(target < sarr[middle]) return binarySearch(sarr, target, start, middle);
    return -1;
}
```
