## Recursion - quick breakdown

Note: **Not** the article for absolute beginners.

Some facts first - 

**What is recursion?**

Directly from wiki - *In computer science, recursion is a method of solving a computational problem where the solution depends on solutions to smaller instances of the same problem. Such problems can generally be solved by iteration, but this needs to identify and index the smaller instances at programming time.*

tl;dr

Calling the same function again and again with different set of arguments each time that breaks down the problem in smaller instances until the problem itself returns a solution.

Let's move on...

Recursion uses an internal stack. The function calls stack up one after the other until the last one starts returning something which in turn makes the next in the stack return because duh, they are the same function. (It's a cool domino effect)

**Space Complexity** - determined by how many times the function gets called.

Maybe an image from google will help visualise

![0_aPCs0hP0Q-s4fkCJ.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1644774979777/cPh-bikRJ.jpeg)

Let's take a cooler example with even cooler visualisation

**Question** -> Find the nth fibonacci number

```javascript
/* 
 * Linear recurrence relation -> Fib(n) = Fib(n-1) + Fib(n-2)
 */
function fibonacci(n){
    if(n<2){ // base condition - represented by answers we already have
        return n;     // in this case we know Fib(0)=0 and Fib(1)=1
    }
    return fibonacci(n-1) + fibonacci(n-2); // add the previous two
}
```

FYI - Fibonacci series goes like this:

`0,1,1,2,3,5,8,13...`

Let's break it down,

Given: <br>
Fib(0) = 0 <br>
Fib(1) = 1  <br>

Try to derive a recurrence relation - we know that the sum of previous two numbers will give the next number. Previous numbers are fibonacci numbers. So sum of previous two fibonacci numbers will give the next fibonacci number.

i.e. `Fib(n) = Fib(n-1) + Fib(n-2)`

Now, we come at a point where we need to return something from the function in order for the functions below to return what they have calculated till now.

The point of return is the base condition. By observation we can see that we know `Fib(0) = 0` and `Fib(1) = 1` which are our given. So this will be our point of return to the base of the stack or to the top of the recursion tree (visualisation coming up).

```
if(n<2) return n;
```

Check the execution sequence given by the numbers on each node


![zmshy.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1644859654891/ItFl6zB8S.png)

Travel up when the function starts returning a value rather than calling a function i.e when you reach leaf node. Here's a debugger output if you don't believe what you are seeing. You can add a `console.log` in the first line of the function and check for yourself.

```
// debugger output 
fib( 5 ) // pass 1
fib( 4 ) // pass 2
fib( 3 ) // pass 3
fib( 2 ) // pass 4
fib( 1 ) // pass 5
fib( 0 ) // pass 6
fib( 1 ) // pass 7
fib( 2 ) // pass 8
fib( 1 ) // pass 9
fib( 0 ) // pass 10
fib( 3 ) // pass 11
fib( 2 ) // pass 12
fib( 1 ) // pass 13
fib( 0 ) // pass 14
fib( 1 ) // pass 15
```


That's it!

