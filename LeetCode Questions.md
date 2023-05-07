# LeetCode Questions


### #1. **Two Sum**

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/two-sum/)

```jsx
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let results = []
    for(let i = 0;i < nums.length;i++) {
        for(let j = i+1;j < nums.length;j++) {
            if(nums[i] + nums[j] == target) {
                results.push(i, j)
            }
        }
    }
    return results
};

// Runtime: 166 ms
// Beats: 23.61%
// Memory: 42.3 MB
// Beats: 74.20%
```

### #9. **Palindrome Number**

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/palindrome-number/)

```jsx
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    let revNumber = 0;
    let number = x;
    if((Math.sign(x)) < 0) {
        return false
    } else {
        while (number > 0) {
            revNumber = (revNumber * 10) + (number % 10);
            number = Math.floor(number / 10);
        }
        if(revNumber == x) {return true
        } else {return false};
    }
};

// Runtime: 168 ms
// Beats: 81.76%
// Memory: 50.1 MB
// Beats: 91.56%
```

### #13. **Roman to Integer**

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/roman-to-integer/)

```jsx
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
    const sym = {
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000
    }
    let result = 0;

    for (let i = 0; i < s.length; i++) {
        const cur = sym[s[i]];
        const next = sym[s[i + 1]];

        if (cur < next) {
            result += next - cur;
            i++;
        } else {
            result += cur;
        }
    }
    return result;
};

// Runtime: 107 ms
// Beats: 98.19%
// Memory: 46.7 MB
// Beats: 65.84%
```

### ****How to Implement a Hash Table Data Structure in JavaScript:****

```jsx
class HashTable {
  constructor() {
    this.table = new Array(127);
    this.size = 0;
  }

  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % this.table.length;
  }

  set(key, value) {
    const index = this._hash(key);
    this.table[index] = [key, value];
    this.size++;
  }

  get(key) {
    const target = this._hash(key);
    return this.table[target];
  }

  remove(key) {
    const index = this._hash(key);

    if (this.table[index] && this.table[index].length) {
      this.table[index] = [];
      this.size--;
      return true;
    } else {
      return false;
    }
  }
}
```

### #**217. Contains Duplicate**

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/contains-duplicate/)

```jsx
/**
 * Hash Set
 * Time O(N) | Space O(N)
 * https://leetcode.com/problems/contains-duplicate/
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = (nums) => {
    const numsSet = new Set(nums);/* Time O(N) | Space O(N) */
    const isEqual = numsSet.size === nums.length;

    return !isEqual;
};

// Runtime: 84 ms
// Beats: 93.2%
// Memory: 54.9 MB
// Beats: 31.52%

/**
 * Hash Set - Early Exit
 * Time O(N) | Space O(N)
 * https://leetcode.com/problems/contains-duplicate/
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = (nums, numsSet = new Set()) => {
    for (const num of nums) {/* Time O(N) */
        if (numsSet.has(num)) return true;

        numsSet.add(num);       /* Space O(N) */
    }

    return false;
};

// Runtime: 82 ms
// Beats: 95.2%
// Memory: 55.5 MB
// Beats: 17.6%

/**
 * Brute Force - Linear Search
 * Time O(N^2) | Space O(1)
 * https://leetcode.com/problems/contains-duplicate/
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = (nums) => {
    for (let right = 0; right < nums.length; right++) {/* Time O(N) */
        for (let left = 0; left < right; left++) {         /* Time O(N) */
            const isDuplicate = nums[left] === nums[right];
            if (isDuplicate) return true;
        }
    }

    return false;
}

/**
 * Sort - HeapSort Space O(1) | QuickSort Space O(log(N))
 * Time O(N * log(N)) | Space O(1)
 * https://leetcode.com/problems/contains-duplicate/
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = (nums) => {
    nums.sort((a, b) => a - b);/* Time O(N * log(N)) | Space O(1 || log(N)) */

    return hasDuplicate(nums);
}

const hasDuplicate = (nums) => {
    for (let curr = 0; curr < (nums.length - 1); curr++) {/* Time O(N) */
        const next = (curr + 1);

        const isNextDuplicate = nums[curr] === nums[next];
        if (isNextDuplicate) return true;
    }

    return false;
}
```

### #**242. Valid Anagram**

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/valid-anagram/)

```jsx
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    if(s.length != t.length) { return false }
    return (getSorted(s) == getSorted(t) ?  true : false)
};

const getSorted = (str) => {
    return str.split('').sort().join('')
}

// Runtime: 107 ms
// Beats: 37%
// Memory: 48 MB
// Beats: 30.35%

/**
 * Sort - HeapSort Space O(1) | QuickSort Space O(log(N))
 * Time O(N * logN) | Space O(N)
 * https://leetcode.com/problems/valid-anagram/
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = (s, t) => {
    const isEqual = s.length === t.length;
    if (!isEqual) return false;

    return reorder(s) === reorder(t); /* Time O(N * logN) | Space O(N) */
};

const reorder = (str) => str
    .split('')                         /* Time O(N)          | Space O(N) */
    .sort((a, b) => a.localeCompare(b))/* Time O(N * log(N)) | Space O(1 || log(N)) */
    .join('');                         /* Time O(N)          | Space O(N) */

/**
 * Hash Map - Frequency Counter
 * Time O(N) | Space O(N)
 * https://leetcode.com/problems/valid-anagram/
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = (s, t, map = new Map()) => {
    const isEqual = s.length === t.length;
    if (!isEqual) return false;

    addFrequency(s, map);      /* Time O(N) | Space O(N) */
    subtractFrequency(t, map); /* Time O(N) | Space O(N) */

    return checkFrequency(map);/* Time O(N) */
};

const addFrequency = (str, map) => {
    for (const char of str) {/* Time O(N) */
        const count = (map.get(char) || 0) + 1;

        map.set(char, count);   /* Space O(N) */
    }
}

const subtractFrequency = (str, map) => {
    for (const char of str) {/* Time O(N) */
        if (!map.has(char)) continue;

        const count = map.get(char) - 1;

        map.set(char, count);   /* Space O(N) */
    }
};

const checkFrequency = (map) => {
    for (const [ char, count ] of map) {/* Time O(N) */
        const isEmpty = count === 0;
        if (!isEmpty) return false;
    }

    return true;
}

// Runtime: 59 ms
// Beats: 99.73%
// Memory: 45.7 MB
// Beats: 41.23%
```
