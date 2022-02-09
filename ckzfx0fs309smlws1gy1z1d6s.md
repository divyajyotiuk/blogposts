## Sorting

### Bubble sort

In-place sorting algorithm, compares adjacent elements in every pass,
sorts the **largest** number first and places in the end. Also known as **sinking sort**, **exchange sort**.

It is a stable sorting algorithm i.e. order in which the number comes should be the same if the value is same.

```
10~, 40, 5, 30, 10
```
after sorting, `10~` with tilde comes before in order of `10` without tilde as it was coming for the unsorted array i.e. order of number `10` is maintained
```
5, 10~, 10, 30, 40
```

Space complexity - **O(1)** (for `temp` variable)

Time complexity

- Best case -  **O(n)** (when array is already sorted)
- Worst case - **O(n^2)** (when array is sorted in opposite)

```javascript
function bubbleSort(nums){
    let n = nums.length;
    let isSwapped = false;
    for(let i=0; i<n; i++){ // passes
        for(let j=1;j<=n-i-1;j++){
            if(nums[j-1]>nums[j]){ // if prev is greater than curr then swap(j-1,j)
                let temp = nums[j];
                nums[j] = nums[j-1];
                nums[j-1] = temp;
                isSwapped = true;
            }
        }
        if(!isSwapped){
            break;
        }
    }
    return nums;
}
```

### Selection sort

Selects an element and places it into its correct position. Not a stable algorithm.

Time complexity - **O(n^2)** (worst and best case both)

```javascript
function selectionSort(nums){
    let n = nums.length;
    for(let i=0; i<n; i++){
        let minIndex = i;
        for(let j=i+1;j<n;j++){ // passes for selecting max/min element
            if(nums[minIndex] > nums[j]){
                minIndex = j;
            }
        }
        let temp = nums[i];
        nums[i] = nums[minIndex];
        nums[minIndex] = temp;
    }
    return nums;
}
```





<!-- ### some sort - WIP

```javascript
function someSort(nums){
    let n = nums.length;
    for(let i=0; i<n; i++){
        for(let j=i+1;j<n;j++){
                console.log(nums[i],nums[j]);
            if(nums[i]>nums[j]){    // swap(i,j)
                let temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }
        }
    }
    return nums;
}
```
-->
