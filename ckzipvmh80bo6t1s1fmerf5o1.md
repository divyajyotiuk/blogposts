## Cyclic sort

This is a very important algorithm for coding interviews.

**Tips **

The pattern of questions that are cues for using this algorithm is - when range is given from `1 to N` or `0 to N`

Time complexity - **O(n)**

Gives O(1) of space complexity. In worst case, makes (2n-1) comparisons

```javascript
function cyclicSort(nums){
    let index = 0;
    while(index < nums.length){
        let pos = nums[index]-1; // pos is the correct position of nums[index]
        if(nums[index] != nums[pos]){
            // place nums[index] in its correct position
            let temp = nums[pos]; // swap
            nums[pos] = nums[index];
            nums[index] = temp;
        }else{
            index=index+1;
        }
    }
    return nums;
}
```

Pass walkthrough for worst case scenario -
```
[ 3, 5, 2, 1, 4 ] // index 0 - given array
[ 2, 5, 3, 1, 4 ] // index 0
[ 5, 2, 3, 1, 4 ] // index 0
[ 4, 2, 3, 1, 5 ] // index 0
[ 1, 2, 3, 4, 5 ] // index 0 at correct position
[ 1, 2, 3, 4, 5 ] // index 1 at correct position
[ 1, 2, 3, 4, 5 ] // index 2 at correct position
[ 1, 2, 3, 4, 5 ] // index 3 at correct position
[ 1, 2, 3, 4, 5 ] // index 4 - final array
```