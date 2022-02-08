## Search in Matrix

### Search in Matrix

There are `m` rows and `n` columns in a matrix. The matrix is row-wise and column-wise sorted. 

```javascript
//0    1     2     3
  0    11    22   33   //0
  16   27    38   49   //1
  32   43    54   65   //2
  48   59    70   81   //3
  64   75    86   97   //4
```

Time complexity - **O(m+n)**

```javascript
function search(arr,target){
    let m = Object.keys(arr).length; // rows
    let n = Object.keys(arr[0]).length; // cols
    let row=0, col=n-1;
    while(row < m && col > 0){
        if(target == arr[row][col]){
            return [row,col];
        }else if(target < arr[row][col]){
            col = col - 1; // eliminate column
        }else{
            row = row + 1; // eliminate row
        }
    }
    return [-1,-1];
}
```

### Binary search in matrix

Sorted Matrix

```javascript
//0    1     2     3
  0    11    22   33   //0
  35   43    54   65   //1
  67   75    86   97   //2
```

Time complexity - **O(logm + logn)**

```javascript
function matrixSearch(nums, target){
    let m = Object.keys(nums).length; // gives #rows
    let n = Object.keys(nums[0]).length; // gives #columns

    let row = binarySearchCol(nums, target, n-1); // give last column and get row
    let col = binarySearchRow(nums, target, row); // search element in that row

    if(nums[row][col] == target) return [row, col];

    return [-1, -1];
}

// returns row which possibly contains the target
function binarySearchCol(nums, target, col){
    let s = 0, n = Object.keys(nums[0]).length, e = n - 1;
    
    while(s<=e){
        let m = Math.floor((s+e)/2);
        if(target == nums[m][col]){
            return m;
        }else if(target < nums[m][col]){
            e = m - 1;
        }else{
            s = m + 1;
        }
    }
    return s;
}

function binarySearchRow(nums, target, row){
    let s = 0, n = Object.keys(nums).length, e = n - 1;
    
    while(s<=e){
        let m = Math.floor((s+e)/2);
        if(target == nums[row][m]){
            return m;
        }else if(target < nums[row][m]){
            e = m - 1;
        }else{
            s = m + 1;
        }
    }
    return s;
}
```

