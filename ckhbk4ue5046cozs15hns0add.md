## Credit card number check

For people building an e-commerce website, a payment portal from scratch, here's some thing which you'll find useful! No plugins required!


This is the **luhn algorithm** or **luhn formula** that checks if the credit card number is valid or not. You'll find this built-in validator in almost all payment processing platforms, like _Stripe_, _Paypal_ to name a few.


### The Algorithm
1. Starting from the second last digit, moving left double the value of every second digit.
2. If the doubled result is greater than 9, subtract 9 from the doubled result
3. Find sum all the digits
4. Take the modulo 10 of the sum and if it equates to 0, then the number is valid according to the algorithm.

### An Example
Take 79927398713 as an example, walkthrough of the algorithm is as follows:
|7|9|9|2|7|3|9|8|7|1|3|
1. |7|**18**|9|**4**|7|**6**|9|**16**|7|**2**|3|
2. |7|**9**|9|4|7|6|9|**7**|7|2|3|
3. Sum of all digits = 70
4. 70%10 = 0 Therefore, valid number.


Here's a javascript implementation depicting use of map and reduce. You can try in your favourite language as well!
```js
function luhn(no){
    no = no.toString();
    arr = no.split('').map(x=>parseInt(x));
    arr.reverse();
    rArr = rArr.map(function(x,index){
    if(index%2!=0){
        if(x*2 >= 10) x = x*2 - 9;
        else x = x*2; 
        }
        return x;
    });
    sum = rArr.reduce((accu,curr)=>accu+curr);
    if(sum%10==0) return true;

    return false; 
}
```

If you wish to know more about this algorithm, you can read more about this [here](https://en.wikipedia.org/wiki/Luhn_algorithm).