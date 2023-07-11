# Common JS Tasks

## Write your own debounce
```javascript
const fetchUrl = (url) => {
  console.log('fetching', url);
}

const debounce = (callback, delay) => {
  let timer = null;
  return (...args) => {
      if (timer) clearTimeout(timer);

      timer = setTimeout(() => {
          callback(...args)
      }, delay);
  }
}

const fetching = debounce(fetchUrl, 300);

fetching('https://google.com');
fetching('https://google.com');
fetching('https://google.com');
fetching('https://google.com');
```

## Grab all values in array
```javascript
const tree = {
  value: 1,
  children: [
    {
      value: 2,
      children: [
        { value: 3 }
      ]
    },
    {
      value: 4,
      children: [
        { value: 5 },
        { value: 6 }
      ]
    }
  ]
}

const getAllValues = (tree) => {
  const values = [];
  const stack = [tree];

  while(stack.length > 0) {
    const node = stack.pop();

    if (node.value) {
      values.push(node.value)
    }

    if (node.children?.length > 0) {
      stack.push(...node.children);
    }
  }

  return values;
}
```
## Write carrying sum. sum(1)(2)(3)...(n) => return 1 + 2 + 3 + ... + n
Approach 1
```javascript
function sum(a) {

  let currentSum = a;

  function f(b) {
    currentSum += b;
    return f;
  }

  f.toString = function() {
    return currentSum;
  };

  return f;
}

console.log(sum(1)(2)(4)(1)(2)(4).toString())
```

Approach 2
```javascript
const sum = (a) => {
  return (b) => {
    if (b) {
      return sum(a + b);
    }
    return a;
  }
}

console.log(sum(1)(2)(4)())
```

## Maximum subarray sum. [1, 2, 3, -5, 6, 7] => 13
```javascript
const maxSubArray = (nums) => {
    let maxSum = -Infinity
    let currentSum = 0
    for(let i = 0; i < nums.length; i++){ 
        currentSum = Math.max(nums[i], currentSum + nums[i])

        maxSum = Math.max(currentSum, maxSum)
        
    }
    return maxSum
}

console.log(maxSubArray([-1, 2, 5, 4, -5]))
```

## Given a string, reverse each word in the sentence
```javascript
function reverseBySeparator(string, separator = "") {
  return string.split(separator).reverse().join(separator);
}

console.log(reverseBySeparator('Hello, my name is Yaro'))
```

## Check if Palindrome
```javascript
function isPalindrome(str) {
	return str == str.split('').reverse().join('');
}
console.log(isPalindrome('level')) // true
```
