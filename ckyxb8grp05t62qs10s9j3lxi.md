## Binary Search

Given a **sorted** array, perform binary search.

Time Complexity - **O(log n)**


**With recursion**

```javascript
function binarySearch(sarr=[], target, start, end){
    if(!sarr.length) return -1;
    let middle = Math.floor((start+end)/2);
    if(sarr[middle] == target) return middle;
    if(target < sarr[middle]) return binarySearch(sarr, target, start, middle - 1);
    if(target > sarr[middle]) return binarySearch(sarr, target, middle + 1, end);
    return -1;
}
```

**Without recursion**

```javascript
function binarySearch(sarr=[], target){
    if(!sarr.length) return -1;

    let start = 0;
    let end = sarr.length - 1;
 
    while(start <= end){
         let middle = Math.floor((start+end)/2);
         if(target < sarr[middle]){ 
             end = middle - 1;
         }else if(target > sarr[middle]){
             start = middle + 1;
         }else{
             return middle;
         }
    }
   
    return -1;
}
```

**Order-agnostic binary search**

When you don't know if the array is sorted in ascending order or descending order.

```javascript
function binarySearch(sarr=[], target, start, end){
    if(!sarr.length) return -1;
    let isAsc = sarr[start] < sarr[end]; // check
    let middle = Math.floor((start+end)/2);
    if(sarr[middle] == target) return middle;
    if(isAsc){
         if(target < sarr[middle]) return binarySearch(sarr, target, start, middle - 1);
         if(target > sarr[middle]) return binarySearch(sarr, target, middle + 1, end);
    }else{
         // reverse the comparison
         if(target > sarr[middle]) return binarySearch(sarr, target, start, middle - 1);
         if(target < sarr[middle]) return binarySearch(sarr, target, middle + 1, end);
    }

    return -1;
}
```


**Tips**

To avoid integer overflow in some languages - 

`middle` can be calculated as:
```
int middle = start + (end - start)/2;
```