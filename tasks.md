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
