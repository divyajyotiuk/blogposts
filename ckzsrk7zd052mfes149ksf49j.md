## Sorting - part 2

### Merge Sort

Not an in-place algorithm. Merge sort preferred for linked list as memory allocation is in a heap.

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

### Quick Sort

About - Not a stable algorithm, In-place and preferred over merge sort

**Pivot** - A pivot `p` is an element in array which after every pass contains elements < `p` to the left hand side of `p` and elements > `p` to the right hand side. 

After every pass pivot is getting placed at the correct position.

*How to put pivot at correct position? *
<br>
- Keep two pointers `s` and `e`
- Check if `a[s] < p` and `a[e] > p`, if not swap(a[s],a[e]) and update the pointers.

Recurrence relation for Quick Sort
```
T(N) = T(k) + T(N-k-1) + O(n) 
/* 
k elements to LHS of pivot 
N-k-1 elements to RHS of pivot 
O(n) time to place pivot at correct position
NOTE: we are not including pivot in LHS or RHS
*/
```

Time complexity

- Worse Case Complexity - **O(n^2)** <br>
When pivot is either largest or smallest element of the array. Reason - recursion size of array becomes (n-1) i.e k=0 in above recurrence relation making it a linear recurrence relation

- Best Case Complexity - **O(n*logn)** <br>
When pivot divides the array in two halves
```
T(N) = T(N/2) + T(N/2) + O(n)
```

Code

```javascript
let arr = [8,4,9,2,3,12,10];

function quickSort(a,low,high){

    if(low >= high){
        return;
    }

    let m = low + parseInt((high - low)/2);
    let pivot = a[m];

    let s = low, e = high; // low,high are start and end of array resp
                            // s & e are pointers 

    while(s <= e){

        while(a[s] < pivot){
            s=s+1;
        }

        while(a[e] > pivot){
            e=e-1;
        }

        // else condition where a[s] > pivot && a[e] < pivot
        // swap
        if(s<=e){
            let temp = a[s];
            a[s] = a[e];
            a[e] = temp;
    
            s=s+1;
            e=e-1;
        }
    }

    quickSort(a,low,e);
    quickSort(a,s,high);
}

let n = arr.length;
quickSort(arr,0,n-1);
```

















