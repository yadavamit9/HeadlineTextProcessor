# Javascript Task:
- __Task__: Modify the throttle function from lodash such that it attempts to get a true response from the function at most N times. Name the function as retry
- __Arguments__:
   - func (Function): The function to invoke. It should return a true or false.
   - [times=1] (Number): Optional.
               The maximum number of times to invoke the function to get a success response with a default number of 1
   - Returns(Boolean): Returns true if the func returns a success response, false otherwise.

__Example__:
```js
let f = () => {
  let d = new Date(); // current time
  return d.getMilliseconds() % 2 == 0; // => true or false
};
_.retry(f, 3);       //=>  true
```

## Solution:

```js
function retry(func, times) {
    /// monitor the count
    var calledCount = 0;

    if(!times){
      times = 1;
    }

    /// creating a clousre (will be called)
    return function(){
        /// checking the limit (if limit is exceeded then do not call the passed function)
        if (times > calledCount) {
            /// increase the count
            calledCount++;
            func();
        }
    };
}
```


## Usage:

- creating a function to pass in the retry function

```js
function myCustomFunction(){
 let d = new Date(); // current time
  return d.getMilliseconds() % 2 == 0; // => true or false
 }

// calling the retry function
retry(myCustomFunction, 3);
```