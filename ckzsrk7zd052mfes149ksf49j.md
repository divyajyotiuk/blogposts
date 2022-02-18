## Sorting - part 2

### Merge Sort

Not an in-place algorithm.

Steps -

- Keep dividing the array into 2 parts recursively till only one element in each array

```javascript
function mergeSort(a){
    if(a.length == 1){
        return a;
    }

    let m = parseInt(a.length/2);

    // Array.prototype.slice provides shallow copy of array. 
    // specify start and end and end is exclusive
    let first = mergeSort(a.slice(0,m));
    let second =  mergeSort(a.slice(m,a.length));

    return merge(first, second);
}

```

- Merge the arrays using two pointers to return a new array 

```javascript
function merge(first=[], second=[]){
    let mergedArr = [];

    let i=0,j=0;

    while(i<first.length && j<second.length){
        if(first[i] < second[j]){
            mergedArr.push(first[i]);
            i=i+1;
        }else{
            mergedArr.push(second[j]);
            j=j+1;
        }
    }

    while(i<first.length){
        mergedArr.push(first[i]);
        i=i+1;
    }

    while(j<second.length){
        mergedArr.push(second[j]);
        j=j+1;
    }

    return mergedArr;
}
```

Space Complexity - **O(n)**

Time Complexity - **O(n*logn)** 
<br> no. of levels = logn 
<br> no. of comparisons at each level = n


### Merge sort - In place

```javascript
let arr = [8,4,9,2,3,12,10];

function mergeSortInPlace(a,s,e){
    console.log("mergeSort(",a,s,e,")");

    if(e-s == 1){
        return;
    }

    let m = s + parseInt((e-s)/2);

    mergeSortInPlace(a,s,m);
    mergeSortInPlace(a,m,e);

    // i -> start of first array
    // j -> start of second array
    let i=s,j=m;

    let mergedArr = [];
    while(i<m && j<e){
        if(arr[i] < arr[j]){
            mergedArr.push(arr[i]);
            i=i+1;
        }else{
            mergedArr.push(arr[j]);
            j=j+1;
        }
    }

    while(i<m){
        mergedArr.push(arr[i]);
        i=i+1;
    }

    while(j<e){
        mergedArr.push(arr[j]);
        j=j+1;
    }

    // 
    for(let k=0;k<mergedArr.length;k++){
        arr[s+k] = mergedArr[k];
    }
}

let n = arr.length;
mergeSortInPlace(arr,0,n);
console.log(arr);
```






