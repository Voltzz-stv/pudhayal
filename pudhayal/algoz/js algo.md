YT - https://youtu.be/ufBbWIyKY2E?si=FP9ZmwGLlnFpVk7Y

The source material is a course designed to prepare beginners for coding interviews by tackling ten important JavaScript algorithms and challenges.

Here are the questions, explanations, and solved JavaScript codes discussed in the source:
**Explanation & Logic:** The fundamental approach is to convert the string into an array, use the built-in array `reverse` method (which only works on arrays), and then convert the array back into a string using `join`. This sequence of operations can be chained in one line of code.

For reversing an integer, convert the integer to a string (using `.toString()`), apply the same reversal methods (`split`, `reverse`, `join`), parse the resulting string back into an integer (using `parseInt`), and handle the crucial edge case of negative numbers by multiplying the result by the original number's sign (`Math.sign(n)`).

**Solved Code (String - Built-in Method Chaining):** This is the cleaner, preferred solution utilizing JavaScript chaining.

```js
function reverseString(str) {
  // Convert string to array, reverse array, join back to string
  return str.split('').reverse().join('');
}
```

**Solved Code (String - Loop Method):** An alternative solution using a `for...of` loop is provided in case the interviewer restricts the use of built-in functions.

```js
function reverseString(str) {
  let reversed = ""; //
  for (let char of str) { // Loop through each character
    reversed = char + reversed; // Insert the current character before the previous characters
  }
  return reversed; //
}
```

**Solved Code (Integer):**

```js
function reverseInt(n) {
  // Convert to string, reverse, join, then parse back to int
  const reversed = parseInt(n.toString().split('').reverse().join(''));

  // Multiply by Math.sign(n) to handle negative numbers, ensuring the sign is correct
  return reversed * Math.sign(n);
}
```

---

### 2. Palindromes

**Question:** Given a string, return `true` if the string is a palindrome (forms the same word if reversed) or `false` if it is not.

**Explanation & Logic:** Since the method for string reversal is already known, the solution involves reversing the input string and checking if the original string is strictly equal to the reversed string. This comparison returns a boolean value directly.

**Solved Code:**

```js
function isPalindrome(str) {
  // Reverse the string using the chaining method
  const reversed = str.split('').reverse().join('');

  // Return the result of the comparison
  return str === reversed;
}
```

---

### 3. Max Character

**Question:** Given a string, return the character that is most commonly used in the string.

**Explanation & Logic:** This problem requires a data structure to maintain the count of each character, known as a **character map** (a JavaScript object is used here).

1. Loop over the string and populate the `charMap`. If the character already exists, increment the count; otherwise, initialize the count to 1.
2. Loop over the object keys using `for...in` syntax.
3. Keep track of the running maximum count (`max`) and the corresponding character (`maxChar`). If the current character's value in the map is greater than `max`, update both `max` and `maxChar`.

**Solved Code (Refactored):**

```js
function maxChar(str) {
  const charMap = {}; //

  // 1. Create the character map (using short-hand conditional assignment)
  for (let char of str) { //
    // If charMap[char] exists, increment it, otherwise set it to 1
    charMap[char] = charMap[char] + 1 || 1;
  }

  let max = 0; //
  let maxChar = ''; //

  // 2. Loop through the object using 'for...in'
  for (let key in charMap) {
    // 3. Check for the maximum value
    if (charMap[key] > max) {
      max = charMap[key]; // Update max count
      maxChar = key; // Update max character
    }
  }

  return maxChar; //
}
```

---

### 4. Chunking an Array

**Question:** Given an array and a chunk size, divide the array into many subarrays where each subarray is of length `size`.

**Explanation & Logic:** The key component is the `slice` array method, which returns a shallow copy of a portion of an array. The approach uses a `while` loop and an `index` variable initialized to 0.

1. The loop continues as long as `index` is less than the array length.
2. Inside the loop, `array.slice(index, index + size)` is used to extract the chunk, which is then pushed into the `result` array.
3. The `index` must be incremented by `size` in each iteration to move to the start of the next chunk.

**Solved Code:**

```js
function chunk(array, size) {
  const result = []; // Array to store the final chunks
  let index = 0; // Index variable starts at 0

  while (index < array.length) { // Loop until the index exceeds the array length
    // Slice extracts elements from 'index' up to 'index + size'
    result.push(array.slice(index, index + size));
    index += size; // Increment index by the chunk size
  }

  return result;
}
```

---

### 5. Capitalization (Title Case)

**Question:** Write a function that accepts a string, capitalizes the first letter of each word in the string, and returns the capitalized string.

**Explanation & Logic:**

1. The input string is split into an array of words using the space delimiter.
2. The array's built-in `map` method is used to iterate over each word, which provides a cleaner solution than using a traditional loop.
3. Inside the map, the first character of the word (`word`) is converted to uppercase.
4. This capitalized first character is concatenated with the rest of the word, which is obtained using `word.slice(1)`.
5. Finally, the resulting array of capitalized words is joined back into a single string using a space delimiter.

**Solved Code (Using Map Method):**

```js
function capitalize(str) {
  const words = str.split(' '); // Split string into an array of words

  // Map iterates over the array and returns a new array with the transformed words
  const capitalizedWords = words.map(word => {
    // Capitalize the first letter (index 0)
    // Concatenate with the rest of the word (from index 1 onward)
    return word.toUpperCase() + word.slice(1);
  });

  return capitalizedWords.join(' '); // Join the array back into a string with spaces
}
```

---

### 6. Anagrams

**Question:** Check if two provided strings are anagrams of each other (using the same characters in the same quantity, ignoring spaces/punctuation, and treating case insensitively).

**Solution 1: Character Map Comparison**

**Explanation & Logic:** This solution uses a helper function to create a character map for each string. The helper function first converts the string to lowercase and removes punctuation and spaces using a regular expression (`/[^\w]/g`).

After creating both maps, the function follows three steps:

1. Compare the length of the keys (unique characters) in both maps. If they don't match, they are not anagrams, and `false` is returned.
2. Loop through the keys of the first map (using `for...in`).
3. Compare the count (value) for that key in map A against map B. If the counts are unequal, return `false`. If both checks pass, return `true`.

**Solved Code 1 (Character Map):**

```js
// Helper function to create character map
function charMap(str) {
  // Convert to lowercase and remove non-word characters (punctuation/spaces)
  const cleanedStr = str.toLowerCase().replace(/[^\w]/g, '');
  const map = {};

  for (let char of cleanedStr) {
    map[char] = map[char] + 1 || 1; // Build the map
  }
  return map;
}

function anagrams(stringA, stringB) {
  const mapA = charMap(stringA);
  const mapB = charMap(stringB);

  // 1. Compare number of unique keys (characters)
  if (Object.keys(mapA).length !== Object.keys(mapB).length) {
    return false;
  }

  // 2. Compare counts of each character
  for (let key in mapA) {
    if (mapA[key] !== mapB[key]) { // Check if count is not equal
      return false;
    }
  }

  return true;
}
```

**Solution 2: Sorting**

**Explanation & Logic:** This intuitive solution involves creating a helper function (`cleanStr`) that cleans the input string, converts it to an array, sorts the characters, and joins it back. If the sorted, cleaned versions of both strings are identical, they must be anagrams.

**Solved Code 2 (Sorting):**

```js
// Helper function to clean and sort the string
function cleanStr(str) {
  return str
    .toLowerCase() // Convert to lowercase
    .replace(/[^\w]/g, '') // Remove punctuation/spaces
    .split('') // Convert to array
    .sort() // Sort the characters
    .join(''); // Join back to string
}

function anagrams(stringA, stringB) {
  // Directly compare the cleaned, sorted strings
  return cleanStr(stringA) === cleanStr(stringB);
}
```

---

### 7. Counting Vowels

**Question:** Write a function that returns the number of vowels (A, E, I, O, U) used in a string.

**Solution 1: Regular Expression**

**Explanation & Logic:** The easiest method uses the built-in string `match` function combined with a regular expression. The regex pattern should include the character set `[aeiou]`, the global flag (`g`) to find all matches, and the case-insensitive flag (`i`). The `match` function returns an array of matches or `null` if none are found. The solution checks if matches exist and returns the length of the array, or 0 otherwise.

**Solved Code 1 (Regex):**

```js
function vowels(str) {
  // Use match with regex: character set [aeiou], global (g), and case insensitive (i) flags
  const matches = str.match(/[aeiou]/gi);

  // If matches exist, return array length; otherwise, return 0
  return matches ? matches.length : 0;
}
```

**Solution 2: Iterative Loop**

**Explanation & Logic:** An alternative solution involves creating an array of vowels (`vowelCheck`) and iterating through the input string.

1. Initialize a `count` variable to 0.
2. Loop through the string, converting each character to lowercase to handle case sensitivity.
3. Use the array helper function `includes` on the `vowelCheck` array to see if the current character is a vowel.
4. If the character is included, increment the `count`.

**Solved Code 2 (Loop):**

```js
function vowels(str) {
  const vowelCheck = ['a', 'e', 'i', 'o', 'u']; //
  let count = 0; //

  for (let char of str) {
    const lowerChar = char.toLowerCase(); // Convert to handle capital letters

    // Check if the lowercase character is included in the vowel array
    if (vowelCheck.includes(lowerChar)) {
      count++; //
    }
  }
  return count;
}
```

---

### 8. FizzBuzz

**Question:** Write a program that console logs numbers from 1 to _n_. Print "Fizz" for multiples of 3, "Buzz" for multiples of 5, and "FizzBuzz" for multiples of both 3 and 5.

**Explanation & Logic:** The solution requires a `for` loop starting from 1 up to _n_. The key to checking for multiples is the **module operator (`%`)**. The conditions must be checked in the correct order:

1. Check for multiples of both 3 AND 5 first.
2. Check for multiples of 3.
3. Check for multiples of 5.
4. Otherwise, log the number itself.

**Solved Code:**

```js
function fizzBuzz(n) {
  for (let i = 1; i <= n; i++) { // Loop from 1 to n

    // 1. Multiples of 3 and 5 (checked first)
    if (i % 3 === 0 && i % 5 === 0) {
      console.log('FizzBuzz');
    }
    // 2. Multiples of 3
    else if (i % 3 === 0) {
      console.log('Fizz');
    }
    // 3. Multiples of 5
    else if (i % 5 === 0) {
      console.log('Buzz');
    }
    // 4. Otherwise, print the number
    else {
      console.log(i);
    }
  }
}
```

---

### 9. Steps

**Question:** Write a function that accepts a positive number _n_ and console logs a step shape with _n_ levels using the pound character (`#`), ensuring spaces on the right-hand side.

**Explanation & Logic:** The problem is solved using **nested loops**: the outer loop handles the rows, and the inner loop handles the columns. Both loops run _n_ times.

1. Initialize an empty string `line` at the start of the outer (row) loop.
2. Inside the inner (column) loop, determine whether to append `#` or a space.
3. The condition for placing a pound symbol is determined by checking if the current `column` index is less than or equal to the current `row` index (`column <= row`).
4. If the condition is met, append `#`; otherwise, append a space.
5. After the inner loop finishes, console log the completed `line`.

**Solved Code:**

```js
function steps(n) {
  // Outer loop iterates rows (starting at 1)
  for (let row = 1; row <= n; row++) {
    let line = "";

    // Inner loop iterates columns (starting at 1)
    for (let col = 1; col <= n; col++) {

      // Condition: Pound symbol placed if column index is less than or equal to row index
      if (col <= row) {
        line += "#";
      } else {
        line += " "; // Space on the right side
      }
    }
    console.log(line);
  }
}
```

---

### 10. Pyramid

**Question:** Write a function that accepts a positive number _n_ and console logs a pyramid shape with _n_ levels using the pound character (`#`), ensuring spaces on both the left and right sides.

**Explanation & Logic:** The solution uses nested loops (rows and columns).

1. **Columns:** The total width (number of columns) is fixed at `2*n - 1`.
2. **Midpoint:** Calculate the center column using `midpoint = Math.floor((2 * n - 1) / 2)`.
3. **Condition:** The pound symbol is placed if the current column index falls within the range determined by the current row number: `column >= midpoint - row` **AND** `column <= midpoint + row`.
4. If the condition is met, append `#`; otherwise, append a space.

**Solved Code:**

```js
function pyramid(n) {
  // Calculate midpoint for 0-indexed column count
  const midpoint = Math.floor((2 * n - 1) / 2);

  // Outer loop iterates rows (0-indexed)
  for (let row = 0; row < n; row++) {
    let line = ""; //

    // Inner loop iterates columns (up to 2*n - 1 total columns)
    for (let column = 0; column < 2 * n - 1; column++) {

      // Condition for placing the pound symbol
      if (column >= (midpoint - row) && column <= (midpoint + row)) {
        line += "#";
      } else {
        line += " "; // Spaces on the left and right
      }
    }
    console.log(line);
  }
}
```

---

### 11. Spiral Matrix

**Question:** Write a function that accepts an integer _n_ and returns that _n_ x _n_ spiral matrix.

**Explanation & Logic:** This challenge involves filling a two-dimensional array (`n` x `n`) in a clockwise spiral pattern.

1. **Initialization:** Create the empty `n` x `n` result matrix. Define boundary variables: `startRow`, `endRow`, `startCol`, `endCol`, and a `counter` (starting at 1).
2. **Looping:** A `while` loop continues as long as the start boundaries do not cross the end boundaries.
3. **Four Sides:** Inside the `while` loop, four sequential `for` loops fill the outermost layer, constantly updating the boundaries to move inward for the next iteration:
    - **Top Row:** Fill left-to-right, then increment `startRow`.
    - **Right Column:** Fill top-to-bottom, then decrement `endCol`.
    - **Bottom Row:** Fill right-to-left, then decrement `endRow`.
    - **Left Column:** Fill bottom-to-top, then increment `startCol`.

**Solved Code:**

```js
function matrix(n) {
  // 1. Initialize result (n x n array of empty arrays)
  const result = [];
  for (let i = 0; i < n; i++) {
    result.push([]);
  }

  // 2. Define Boundary Variables
  let counter = 1;
  let startRow = 0;
  let endRow = n - 1;
  let startCol = 0;
  let endCol = n - 1;

  // 3. Main While Loop (handles inner spirals)
  while (startRow <= endRow && startCol <= endCol) {

    // 4. Top Row (from startCol to endCol)
    for (let i = startCol; i <= endCol; i++) {
      result[startRow][i] = counter;
      counter++;
    }
    startRow++; // Move boundary down

    // 5. Right Column (from startRow to endRow)
    for (let i = startRow; i <= endRow; i++) {
      result[i][endCol] = counter;
      counter++;
    }
    endCol--; // Move boundary left

    // 6. Bottom Row (from endCol down to startCol)
    for (let i = endCol; i >= startCol; i--) {
      result[endRow][i] = counter;
      counter++;
    }
    endRow--; // Move boundary up

    // 7. Left Column (from endRow down to startRow)
    for (let i = endRow; i >= startRow; i--) {
      result[i][startCol] = counter;
      counter++;
    }
    startCol++; // Move boundary right
  }

  return result; //
}
```