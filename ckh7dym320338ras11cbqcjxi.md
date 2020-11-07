## Easy peasy perfect square

The question is to return true if the number is perfect square otherwise false. 
A **perfect square** is an integer that is the square of an integer.
Javascript provides numerous ways to write a code for this. I will let you know that this is what I did:
```
const isSquare = (n) => {
    return (Math.sqrt(n) === Math.ceil(Math.sqrt(n)));
}
```

Below is the solution that impressed me, because it is simple Math my brain couldn't get hold of first: 
```
const isSquare = function(n){
  return Math.sqrt(n) % 1 === 0;
}
```

And it is clever and also follows the best practices!

Checking the datatype would also work using `isInteger`. But you never know when it would get obsolete! Languages change but the Math around remains the same! Choose better!