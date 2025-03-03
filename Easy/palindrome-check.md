# Palindrome Check

### Understanding the problem

We are asked to write a function that is going to determine whether or not a given string is a palindrome, in other words, whether the given string reads the same backward as forward. If a string has zero or one character, it is a palindrome. The input string contains at least one character.

#

### Approach 1: Reverse the input string (Store the reversed version as a string)

If a string is a palindrome, the reversed version of the string is the same as the original one.

```
"racecar"
reversed: "racecar"

"hello"
reversed: "olleh"
```

So to determine whether a string is a palindrome, we can just reverse the input string and compare the reversed string to the original one.

### Implementation

```js
function isPalindrome(string) {
  let reversedString = '';

  for (let i = string.length - 1; i >= 0; i--) {
    reversedString += string[i];
  }

  return reversedString === string;
}
```

### Complexity Analysis

Given N as the length of the string.

- Time Complexity: O(N^2).

  In most programming languages, strings are immutable. When appending a character to a string, a new string must be created, which is an O(N) operation. To create a reversed version of a string of length N, we will append N characters to the reversed string. Thus the overall time complexity is O(N^2).

- Space Complexity: O(N).

#

### Approach 2: Reverse the input string (Store the reversed version as an array of characters)

We can reduce the reverse from O(N^2) to O(N) by using an array to store the reversed version of the input string, since inserting an element at the end of an array is an amortized O(1) operation as long as the array is implemented as a dynamic array.

### Implementation

```js
function isPalindrome(string) {
  const reversedChars = [];

  for (let i = string.length - 1; i >= 0; i--) {
    reversedChars.push(string[i]);
  }

  return reversedChars.join('') === string;
}
```

### Complexity Analysis

Given N as the length of the string.

- Time Complexity: O(N).

- Space Complexity: O(N).

#

### Approach 3: Two Pointers (Iterative)

A string is a palindrome if the right half of the string is a mirror reflection of the left half:

```
string1 = "raccar"

              |
          rac | car
              |


string2 = "racecar"

              |
          rac e car
              |
```

If we start from the middle of a palindrome and traverse outwards, we would encounter the same characters in the exact same order in both halves.

```
r a c c a r
    ^ ^

r a c c a r
  ^     ^

r a c c a r
^         ^
```

This observation naturally leads to a two-pointer approach. We can initialize one pointer to the start of the string and the other pointer to the end of the string. Then we walk from both the start and the end of the string to the middle and compare every character against the other. If we reach the middle of the string without any mismatches, then the string is a palindrome.

### Implementation

```js
function isPalindrome(string) {
  let leftIdx = 0;
  let rightIdx = string.length - 1;

  while (leftIdx < rightIdx) {
    if (string[leftIdx] !== string[rightIdx]) return false;

    leftIdx++;
    rightIdx--;
  }

  return true;
}
```

### Complexity Analysis

- Time Complexity: O(N), where N is the length of the string.

- Space Complexity: O(1).

#

### Approach 4: Two Pointers (Recursive)

We can also rewrite the iterative solution above recursively.

### Implementation

```js
function isPalindrome(string, leftIdx = 0) {
  const rightIdx = string.length - 1 - leftIdx;

  if (leftIdx >= rightIdx) return true;

  return (
    string[leftIdx] === string[rightIdx] && isPalindrome(string, leftIdx + 1)
  );
}
```

### Complexity Analysis

Given N as the length of the string.

- Time Complexity: O(N).

- Space Complexity: O(N).
