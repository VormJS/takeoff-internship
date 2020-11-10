- <details>
  <summary>
     ✔️ Типы данных в JS. Typeof Null, typeof NaN.
  </summary>

  - number (Numbers, NaN, Infinity, - Infinity)
  - bigInt (Number more than 2^53)
  - string (chars sequence)
  - boolean (true, false)
  - null (special type for empty values) 
  - undefined (special type for non-defined variables)
  - object (complex type with properties (key-value))
  - symbol (type for unique ids)

  `typeof NaN` - "number"  
  `typeof Null` - "object", but it's language mistake
</details>

- <details>
  <summary>
    ✔️ Приведения типов. Ряд вопросов с примерами.
  </summary>

  - String  
  `String(value)`
    - true/false -> "true"/"false"
    - null -> "null"
    - undefined -> "undefined"
    - object -> [object Object] (except special objects like Arrays, Dates, etc.)
    - number -> number as string
  - Number  
  `Number(value)`
    - true/false -> 1/0
    - null -> 0
    - undefined -> NaN
    - string -> trims whitespaces and gets number (also "" becomes 0) or NaN if non-number symbols
    - object -> NaN (except Dates or Array with one number)
  - Boolean  
  `Boolean(value)`
    - "", 0, false, NaN, null, undefined -> false
    - other -> true
</details>

* <details>
  <summary>
    ✔️ Отличие == от ===
  </summary>

  - == 
  uses non-strict comparison with type conversion
  - ===
  uses strict comparison, different types returns false

  NB:
  ```javascript
  (null == undefined); // true
  (null === undefined); // false
  ```
</details>

* <details>
  <summary>
    ✔️ В чем разница между null и undefined?
  </summary>

  `null` - empty value  
  `undefined` - declared and not assigned variable
</details>

* <details>
  <summary>
    ✔️ В чем разница между переменными, созданными с помощью let, var или const? Хоистинг переменных.
  </summary>

  *let* and *const* may be used inside curved brackets {} where they declared and initialized (ReferenceError otherwise).
  *let* variable can be reassigned, *const* variable cannot be reassigned.  
  *var* have weird and hardly controlled behaviour, better don't use it.  

  Hoisting moves variable declarations to the top of the code. That makes possible to use variables before declaration. But hoisting does not work for initializing. Also hoisting does not working for *let* and *const*.  

  As a good rule: **always declare all variables at the beginning of every scope.**

  strict mode blocks opportunity to use variable before declaration.

</details>

* <details>
  <summary>
  ✔️ Use strict. Что это? Приведите пример разного поведения строго режима и обычного.
  </summary>

  Strict mode makes the code more secure by throwing errors in some cases, which works in standard mode.  
  Activated by using directive only at the beginning of script or function  
  `"use strict";`

  example:
  ```javascript
  str = 'str1'; // creates var str
  ```
  ```javascript
  "use strict";
  str = 'str2'; // cause error
  ```

  List of differences:
    - Using a variable/object, without declaring it, is not allowed
    - Assignment to a non-writable global is not allowed
    - Deleting a variable/object/function is not allowed
    - Duplicating a parameter name(functions)/a property name(objects) is not allowed
    - Octal numeric literals and escape characters are not allowed
    - Writing to a read-only/get-only property of objects is not allowed:
    - Deleting an undeletable property is not allowed
    - The with statement is not allowed
    - Words that can **not** be used as variable:
      - eval
      - arguments
      - implements
      - interface
      - let
      - package
      - private
      - protected
      - public
      - static
      - yield 
</details>

* <details>
  <summary>
    ✔️ Виды функций. Отличие стрелочных функций. Что такое и в чем разница между Function Expression и Function Declaration?
  </summary>

  There are two types of functions based on their creation:
  - Function Declaration
  - Function Expression

  The table below shows the difference:
  | Feature | Function Declaration | Function Expression |
  | --- |:---:| :---:|
  | Function need name (can't be anonymous)  | ✔️ | ❌ |
  | Hoisting | ✔️ | ❌ |
  | Global scoped | ✔️ | ❌ |
  | IIFE (immediately invoked function expressions) | ❌ | ✔️ |
  
   Examples:
   ```javascript
  // Function Declaration
  function doSomething() {
    // code
  };
  // Function Expression
  const doSomething = function() {
    // code
  };
  ```

  Arrow function it's shorthand for Function Expression  
  ```javascript
  const doSomething = function() {/*code*/}; // Standard function expression
  const doSomething = () => {/*code*/}; // Arrow function expression
  ```

</details>

* <details>
  <summary>
    ✔️ Что такое this? Методы привязки контекста и их различие?
  </summary>

  `this` is a reference to the object itself, from which it is called.
  Behaviour depends on where it uses:

  | Place | Reference |
  | :---: |:---:|
  | method  | owner object |
  | global | global object |
  | function | global object (non-strict) /	undefined (strict) |
  | arrow function | keeps previous context |
  | event | element (which have attached event) |
  
  Also, there are methods `call()` and `apply()`.
  They can be used to replace the default `this` object with a given as parameter.
  `bind()` method allows copy function with replaced `this`, that works only once (can’t be replaced again after first `bind()`)

</details>

* <details>
  <summary>
    ✔️ Замыкания. Что это такое? Задачки: написать функцию которая работает таким образом: multiply(7)(3)(2) => 42.
  </summary>

  The `closure` is an instrument to define inner and outer function context. It gives opportunity for a function to get access to outer scope and keep in memory inner scope.

  NB: If there are variables with the same name in outer and inner function scope, function priors inner variable, when it calls (way from inner scope to global scope)

  function:
  ```
  function multiply(number) {
    let savedNumber = 1

    function multiplyBase(num) {
      savedNumber *= num
      return multiplyBase
    }

    multiplyBase.toString = () => savedNumber
  
    return multiplyBase(number);
  }
  ```

</details>

* <details>
  <summary>
    ✔️ Прототипы, прототипное наследование. Перебираем обьект, как определить чье поле, обьекта или прототипа? Написать функцию, которая отработает следующим образом: 4.plus(2).minus(1) => 5
  </summary>

  A `prototype` is an object that grants properties and methods for derivative object. Class inheritance implemented in JavaScript via `prototype inheritance`. Prototypes form a chain till they reach `null` as final link.

  Method `hasOwnProperty()` allow to determine is a given property own or belongs to prototype.  
  The usage `for .. in` cycle combined with `hasOwnProperty()` method might be handy, for example:
  ```javascript
  function determineObjectOwnProps(obj){
    const props = [];
    for (const prop in obj) {
      props.push({property: prop, own: obj.hasOwnProperty(prop)})
    }
    console.table(props);
  }
  ```
  For getting array of own keys might be used `Object.keys()` or `Object.getOwnPropertyNames()` methods.

  For implementing `4.plus(2).minus(1)` we should modify `Number` prototype with additional methods `plus` and `minus`, but the number must be wrapped in the brackets `()` for correct working.
  ```javascript
  Number.prototype.plus = function(num) {return this + num}
  Number.prototype.minus = function(num) {return this - num}
  console.log((4).plus(2).minus(1))
  console.log((120).minus(79).plus(6))
  ```

</details>

---
* <details>
  <summary>
    ✔️ typeof([]). Как отличить массив от обьекта?
  </summary>

  `typeof([])` returns `object`.
  In this case might be used `Array.isArray()` method
  ```javascript
  console.log(Array.isArray([]))
  console.log(Array.isArray({}))
  ```

</details>

* <details>
  <summary>
    ✔️ Как скопировать обьект в другой обьект? Передача по ссылке. Написать функцию которая работает как Object.assign, которая скопирует поля обьекта в другой обьект с любой вложенностью.
  </summary>

  The easiest way for object copying is method `Object.assign()`, but it does not work properly with nested objects (all nested objects keeps links)

  There are different ways for deep copying: using special libraries or using `JSON.parse(JSON.stringify())`.  
  Also, there is an option to write recursive function:
  ```javascript
  function deepCopy(obj) {
    if (typeof obj === 'object' || obj === null) {
      const objCopy = {};
      Object.keys(obj).forEach(prop => {
        objCopy[prop] = deepCopy(obj[prop])
      })
      return objCopy;
    } else if (Array.isArray(obj)) {
      return objCopy = obj.map(elem => {
        return deepCopy(elem);
      });
    } else {
      return obj;
    }
  }
  ```

</details>

* <details>
  <summary>
    ✔️ Методы массивов. (Задачки)
  </summary>

  list of exersises:
  http://sinyakov.com/frontend/problems.html

  <details>
    <summary>
      ✔️ sum-of-positive
    </summary>

    Description:  
    You get an array of numbers, return the sum of all of the positives ones.

    Example [1,-4,7,12] => 1 + 7 + 12 = 20

    Note: if there is nothing to sum, the sum is default to 0.

    Solution:  
    ```javascript
    function positiveSum(arr) {
      return arr.reduce((acc, elem) => {
        return elem > 0 ? acc + elem : acc
      }, 0)
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ shortest-word
    </summary>

    Description:  
    Simple, given a string of words, return the length of the shortest word(s).

    String will never be empty and you do not need to account for different data types.



    Solution:  
    ```javascript
    function findShort(s) {
      return s.split(" ").reduce((minLength, word) => Math.min(minLength, word.length), Infinity);
    }
    ```

  </details>

   <details>
    <summary>
      ✔️ list-filtering
    </summary>

    Description:  
    In this kata you will create a function that takes a list of non-negative integers and strings and returns a new list with the strings filtered out.

    Example:  
    `filter_list([1,2,'a','b']) == [1,2]`  
    `filter_list([1,'a','b',0,15]) == [1,0,15]`  
    `filter_list([1,2,'aasf','1','123',123]) == [1,2,123]`
    
    Solution:  
    ```javascript
    function filter_list(l) {
      return l.filter(elem => typeof elem === 'number')
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ square-every-digit
    </summary>

    Description:  
    Welcome. In this kata, you are asked to square every digit of a number and concatenate them.

    For example, if we run 9119 through the function, 811181 will come out, because 9<sup>2</sup> is 81 and 1<sup>2</sup> is 1.

    Note: The function accepts an integer and returns an integer

    Solution:  
    ```javascript
    function squareDigits(num) {
      return Number(String(num).split('').map(num => num * num).join(''));
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Build a square
    </summary>

    Description:  
    I will give you an integer. Give me back a shape that is as long and wide as the integer. The integer will be a whole number between 1 and 50.

    Example  
    `n = 3`, so I expect a 3x3 square back just like below as a string:

    +++  
    +++  
    +++

    Solution:  
    ```javascript
    function generateShape(integer) {
      return ('+'.repeat(integer) + '\n').repeat(integer - 1) + '+'.repeat(integer);
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Friend or Foe
    </summary>

    Description:  
    Make a program that filters a list of strings and returns a list with only your friends name in it.

    If a name has exactly 4 letters in it, you can be sure that it has to be a friend of yours! Otherwise, you can be sure he's not...

    Ex: Input = ["Ryan", "Kieran", "Jason", "Yous"], Output = ["Ryan", "Yous"]

    i.e.

    ```
    friend ["Ryan", "Kieran", "Mark"] `shouldBe` ["Ryan", "Mark"]
    ```
    Note: keep the original order of the names in the output.    

    Solution:  
    ```javascript
    function friend(friends) {
      return friends.filter(name => name.length === 4);
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Vowel Count
    </summary>

    Description:  
    Return the number (count) of vowels in the given string.

    We will consider `a, e, i, o, u` as vowels for this Kata (but not `y`).

    The input string will only consist of lower case letters and/or spaces.

    Solution:  
    ```javascript
    function getCount(str) {
      var vowelsCount = 0;

      str.split('').forEach(symbol => vowelsCount = vowelsCount + ['a', 'e', 'i', 'o', 'u'].includes(symbol));

      return vowelsCount;
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ playing-with-digits
    </summary>

    Description:  
    Some numbers have funny properties. For example:

    `89 --> 8¹ + 9² = 89 * 1`

    `695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2`

    `46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51`

    Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p

    - we want to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n.
    In other words:

    `Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k`

    If it is the case we will return k, if not return -1.

    Note: n and p will always be given as strictly positive integers.
    ```
    digPow(89, 1) should return 1 since 8¹ + 9² = 89 = 89 * 1
    digPow(92, 1) should return -1 since there is no k such as 9¹ + 2² equals 92 * k
    digPow(695, 2) should return 2 since 6² + 9³ + 5⁴= 1390 = 695 * 2
    digPow(46288, 3) should return 51 since 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
    ```

    Solution:  
    ```javascript
    function digPow(n, p) {
      const sumOfPows = Array.from(String(n), Number).reduce((sum, digit, index) => sum + digit ** (index + p), 0);
      return sumOfPows % n === 0 ? sumOfPows / n : -1
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ array-dot-diff
    </summary>

    Description:  
    Your goal in this kata is to implement a difference function, which subtracts one list from another and returns the result.

    It should remove all values from list a, which are present in list b.  
    `arrayDiff([1,2],[1]) == [2]`  
    If a value is present in b, all of its occurrences must be removed from the other:  
    `arrayDiff([1,2,2,2,3],[2]) == [1,3]`  

    Solution:  
    ```javascript
    function arrayDiff(a, b) {
      return a.filter(elem => !b.includes(elem))
    }    
    ```

  </details>

  <details>
    <summary>
      ✔️ find-the-capitals-1
    </summary>

    Description:  
    Write a function that takes a single string (word) as argument. The function must return an ordered list containing the indexes of all capital letters in the string.

    Example:  
    `Test.assertSimilar( capitals('CodEWaRs'), [0,3,4,6] );`

    Solution:  
    ```javascript
    var capitals = function (word) {
      return word.split('').map((symbol, index) => symbol.match(/[A-Z]/g) ? index : -1).filter(index => index >= 0);
    };
    ```

  </details>

  <details>
    <summary>
      ✔️ insert-dashes
    </summary>

    Description:  
    Write a function insertDash(num)/InsertDash(int num) that will insert dashes ('-') between each two odd numbers in num. For example: if num is 454793 the output should be 4547-9-3. Don't count zero as an odd number.

    Note that the number will always be non-negative (>= 0).

    Solution:  
    ```javascript
    function insertDash(num) {
      const regex = /([1|3|5|7|9])([1|3|5|7|9])/g
      return String(num).replace(regex, "$1-$2").replace(regex, "$1-$2")
    }

    ```

  </details>

  <details>
    <summary>
      ✔️ Count the smiley faces
    </summary>

    Description:  
    Given an array (arr) as an argument complete the function countSmileys that should return the total number of smiling faces.

    Rules for a smiling face:

    Each smiley face must contain a valid pair of eyes. Eyes can be marked as : or ;
    A smiley face can have a nose but it does not have to. Valid characters for a nose are - or ~
    Every smiling face must have a smiling mouth that should be marked with either ) or D
    No additional characters are allowed except for those mentioned.

    Valid smiley face examples: `:) :D ;-D :~)`
    Invalid smiley faces: `;( :> :} :]`

    Example  
    ``` 
    countSmileys([':)', ';(', ';}', ':-D']);       // should return 2;
    countSmileys([';D', ':-(', ':-)', ';~)']);     // should return 3;
    countSmileys([';]', ':[', ';*', ':$', ';-D']); // should return 1;
    ```
    Note  
    In case of an empty array return 0. You will not be tested with invalid input (input will always be an array). Order of the face (eyes, nose, mouth) elements will always be the same.

    Solution:  
    ```javascript
    function countSmileys(arr) {
      return arr.filter(face => face.match(/(\:|\;)(\-|\~)?(\)|D)/)).length
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ homogenous-arrays
    </summary>

    Description:  
    Challenge:

    Given a two-dimensional array, return a new array which carries over only those arrays from the original, which were not empty and whose items are all of the same type (i.e. homogenous). For simplicity, the arrays inside the array will only contain characters and integers.

    Example:

    Given [[1, 5, 4], ['a', 3, 5], ['b'], [], ['1', 2, 3]], your function should return [[1, 5, 4], ['b']].

    Addendum:

    Please keep in mind that for this kata, we assume that empty arrays are not homogenous.

    The resultant arrays should be in the order they were originally in and should not have its values changed.

    No implicit type casting is allowed. A subarray [1, '2'] would be considered illegal and should be filtered out.

    
    Solution:  
    ```javascript
    function filterHomogenous(arrays) {
      return arrays.filter(arr => arr.length > 0 && arr.map(elem => typeof elem).every((val, i , arr) => val === arr[0] ));
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ lottery-ticket
    </summary>

    Description:  
    Time to win the lottery!

    Given a lottery ticket (ticket), represented by an array of 2-value arrays, you must find out if you've won the jackpot. Example ticket:

    ```
    [ [ 'ABC', 65 ], [ 'HGR', 74 ], [ 'BYHT', 74 ] ]
    ```
    To do this, you must first count the 'mini-wins' on your ticket. Each sub array has both a string and a number within it. If the character code of any of the characters in the string matches the number, you get a mini win. Note you can only have one mini win per sub array.

    Once you have counted all of your mini wins, compare that number to the other input provided (win). If your total is more than or equal to (win), return 'Winner!'. Else return 'Loser!'.

    All inputs will be in the correct format. Strings on tickets are not always the same length.

    Solution:  
    ```javascript
    function bingo(tickets, win) {
      return tickets.map(ticket => ticket[0].split('').some(char => char.charCodeAt(0) === ticket[1]) ? true : false).filter(res => res === true).length >= win ? 'Winner!' : 'Loser!'
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ row-weights
    </summary>

    Description:  
    Scenario  
    Several people are standing in a row divided into two teams. The first person goes into team 1, the second goes into team 2, the third goes into team 1, and so on.

    Task  
    Given an array of positive integers (the weights of the people), return a new array/tuple of two integers, where the first one is the total weight of team 1, and the second one is the total weight of team 2.

    Notes  
    Array size is at least 1.
    All numbers will be positive.
    Input >> Output Examples
    ```
    rowWeights([13, 27, 49])  ==>  return (62, 27)
    ```
    Explanation:  
    The first element 62 is the total weight of team 1, and the second element 27 is the total weight of team 2.
    ```
    rowWeights([50, 60, 70, 80])  ==>  return (120, 140)
    ```
    Explanation:  
    The first element 120 is the total weight of team 1, and the second element 140 is the total weight of team 2.

    ```
    rowWeights([80])  ==>  return (80, 0)
    ```
    Explanation:  
    The first element 80 is the total weight of team 1, and the second element 0 is the total weight of team 2.

    Solution:  
    ```javascript
    function rowWeights(array) {
      return array.reduce((result, value, index) => result.map((team, i) => index % 2 === i ? team + value : team), [0, 0])
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ scrolling-text
    </summary>

    Description:  
    Let's create some scrolling text!

    Your task is to complete the function which takes a string, and returns an array with all possible rotations of the given string, in uppercase.

    Example
    `scrollingText("codewars")` should return:
    ```
    [ "CODEWARS",
      "ODEWARSC",
      "DEWARSCO",
      "EWARSCOD",
      "WARSCODE",
      "ARSCODEW",
      "RSCODEWA",
      "SCODEWAR" ]
    ```
    Good luck!

    Solution:  
    ```javascript
    function scrollingText(text) {
      return [...Array(text.length)].map((str, i) => (text.slice(i) + text.slice(0, i)).toUpperCase())
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ zipwith
    </summary>

    Description:  
    Implement zipWith  
    zipWith takes a function and two arrays and zips the arrays together, applying the function to every pair of values.  
    The function value is one new array.

    If the arrays are of unequal length, the output will only be as long as the shorter one.
    (Values of the longer array are simply not used.)

    Inputs should not be modified.

    Examples
    ```javascript
    zipWith( Math.pow, [10,10,10,10], [0,1,2,3] )      =>  [1,10,100,1000]
    zipWith( Math.max, [1,4,7,1,4,7], [4,7,1,4,7,1] )  =>  [4,7,7,4,7,7]

    zipWith( function(a,b) { return a+b; }, [0,1,2,3], [0,1,2,3] )  =>  [0,2,4,6]  Both forms are valid.
    zipWith( (a,b) => a+b, [0,1,2,3], [0,1,2,3] )  =>  [0,2,4,6]  Both are functions.
    ```
    Input validation  
    Assume all input is valid.

    Solution:  
    ```javascript
    function zipWith(fn,a0,a1) {
      return [...Array(Math.min(a0.length, a1.length))].map((el, i) => fn(a0[i], a1[i]));
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ beginner-lost-without-a-map
    </summary>

    Description:  
    Given an array of integers, return a new array with each value doubled.

    For example:

    `[1, 2, 3] --> [2, 4, 6]`

    For the beginner, try to use the map method - it comes in very handy quite a lot so is a good one to know.

    Solution:  
    ```javascript
    function maps(x){
      return x.map(num => num * 2);
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ array-plus-array
    </summary>

    Description:  
    I'm new to coding and now I want to get the sum of two arrays...actually the sum of all their elements. I'll appreciate for your help.

    P.S. Each array includes only integer numbers. Output is a number too.

    Solution:  
    ```javascript
    
    ```

  </details>

  <details>
    <summary>
      ✔️ array-plus-array
    </summary>

    Description:  
    I'm new to coding and now I want to get the sum of two arrays...actually the sum of all their elements. I'll appreciate for your help.

    P.S. Each array includes only integer numbers. Output is a number too.

    Solution:  
    ```javascript
    function arrayPlusArray(arr1, arr2) {
      return arr1.concat(arr2).reduce((sum, el) => sum + el, 0)
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ is-every-value-in-the-array-an-array
    </summary>

    Description:  
    Is every value in the array an array?

    This should only test the second array dimension of the array. The values of the nested arrays don't have to be arrays.

    Examples:
    ```
    [[1],[2]] => true
    ['1','2'] => false
    [{1:1},{2:2}] => false
    ```

    Solution:  
    ```javascript
    const arrCheck = arr => arr.every(el => Array.isArray(el))
    ```

  </details>

  <details>
    <summary>
      ✔️ make-a-square-box
    </summary>

    Description:  
    Easy; Make a box
    Given a number as a parameter, return an array containing strings which form a box.
    Like this:

    n = 5
    ```
    [
      '-----',
      '-   -',
      '-   -',
      '-   -',
      '-----'
    ]
    ```
    n = 3
    ```
    [
      '---',
      '- -',
      '---'
    ]
    ```

    Solution:  
    ```javascript
    function box(num) {
      return [...Array(num)].map((el, i) => i === 0 || i === num - 1 ? '-'.repeat(num) : `-${' '.repeat(num - 2)}-`);
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ magic-index
    </summary>

    Description:  
    A magic index in an array A[1...n-1] is defined to be an index such that A[i] = i. Given a sorted array of distinct integers, write a method to find a magic index, if one exists, in array A.

    ```
    findMagic([-20,-10,2,10,20]); // Returns 2
    ```

    Solution:  
    ```javascript
    function findMagic(arr){  
      const magicNum = arr.filter((el,i) => el === i)[0]
      return magicNum ? magicNum : -1
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ flatten-and-sort-an-array
    </summary>

    Description:  

    Given a two-dimensional array of integers, return the flattened version of the array with all the integers in the sorted (ascending) order.

    Example:

    Given [[3, 2, 1], [4, 6, 5], [], [9, 7, 8]], your function should return [1, 2, 3, 4, 5, 6, 7, 8, 9].

    Addendum:

    Please, keep in mind, that JavaScript is by default sorting objects alphabetically. For more information, please consult:

    http://stackoverflow.com/questions/6093874/why-doesnt-the-sort-function-of-javascript-work-well

    Solution:  
    ```javascript
    function flattenAndSort(array) {
      return [].concat(...array).sort((a,b) => a-b > 0 ? 1 : -1);
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Two Sum
    </summary>

    Description:  
    Write a function that takes an array of numbers (integers for the tests) and a target number. It should find two different items in the array that, when added together, give the target value. The indices of these items should then be returned in a tuple like so: (index1, index2).

    For the purposes of this kata, some tests may have multiple answers; any valid solutions will be accepted.

    The input will always be valid (numbers will be an array of length 2 or greater, and all of the items will be numbers; target will always be the sum of two different items from that array).

    Based on: http://oj.leetcode.com/problems/two-sum/
    ```
    twoSum [1, 2, 3] 4 === (0, 2)
    ```

    Solution:  
    ```javascript
    function twoSum(numbers, target) {
      for (const [i1, el1] of numbers.entries()) {
        const checkResult = numbers.findIndex((el2, i2) => el1 + el2 === target && i2 !== i1)
        if (checkResult !== -1) {
          return [i1, checkResult]
        }
      }
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Length of missing array
    </summary>

    Description:  
    You get an array of arrays.  
    If you sort the arrays by their length, you will see, that their length-values are consecutive.
    But one array is missing!


    You have to write a method, that return the length of the missing array.
    ```
    Example:
    [[1, 2], [4, 5, 1, 1], [1], [5, 6, 7, 8, 9]] --> 3
    ```

    If the array of arrays is null/nil or empty, the method should return 0.

    When an array in the array is null or empty, the method should return 0 too!
    There will always be a missing element and its length will be always between the given arrays.

    Have fun coding it and please don't forget to vote and rank this kata! :-)

    I have created other katas. Have a look if you like coding and challenges.

    Solution:  
    ```javascript
    function getLengthOfMissingArray(arrayOfArrays) {
      if (!arrayOfArrays || arrayOfArrays.some(arr => !arr)) {
        return 0;
      }
      const sortedArray = arrayOfArrays.sort((a, b) => a.length - b.length);
      const minLength = sortedArray[0] && sortedArray[0].length;
      if (minLength) {
        return sortedArray.map((arr, i) => arr.length - i - minLength).findIndex(el => el === 1) + minLength;
      } else {
        return 0;
      }
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Data Reverse
    </summary>

    Description:  
    A stream of data is received and needs to be reversed.

    Each segment is 8 bits long, meaning the order of these segments needs to be reversed, for example:

    ```
    11111111  00000000  00001111  10101010
    (byte1)   (byte2)   (byte3)   (byte4)
    ```
    should become:
    ```
    10101010  00001111  00000000  11111111
    (byte4)   (byte3)   (byte2)   (byte1)
    ```
    The total number of bits will always be a multiple of 8.

    The data is given in an array as such:
    ```
    [1,1,1,1,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,0,1,0,1,0,1,0]
    ```
    Note: In the C and NASM languages you are given the third parameter which is the number of segment blocks.

    Solution:  
    ```javascript
    function dataReverse(data) {
      let resultArr = [];
      for (let i = data.length / 8; i > 0; i--) {
        resultArr = resultArr.concat(data.slice((i - 1) * 8, i * 8));
      }
      return resultArr
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Duplicate Encoder
    </summary>

    Description:  
    The goal of this exercise is to convert a string to a new string where each character in the new string is `"("` if that character appears only once in the original string, or `")"` if that character appears more than once in the original string. Ignore capitalization when determining if a character is a duplicate.

    Examples
    ```
    "din"      =>  "((("
    "recede"   =>  "()()()"
    "Success"  =>  ")())())"
    "(( @"     =>  "))((" 
    ```
    Notes

    Assertion messages may be unclear about what they display in some languages. If you read "...It Should encode XXX", the "XXX" is the expected result, not the input!

    Solution:  
    ```javascript
    function duplicateEncode(word) {
      return word.split('').map((letter, i) => (word.slice(0, i) + word.slice(i + 1)).toLowerCase().includes(letter.toLowerCase()) ? ')' : '(').join('');
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Alternate capitalization
    </summary>

    Description:  
    Given a string, capitalize the letters that occupy even indexes and odd indexes separately, and return as shown below. Index `0` will be considered even.

    For example, `capitalize("abcdef") = ['AbCdEf', 'aBcDeF']`. See test cases for more examples.

    The input will be a lowercase string with no spaces.

    Good luck!

    Solution:  
    ```javascript
    function capitalize(s) {
      return [
        s.split('').map((letter, i) => i % 2 ? letter : letter.toUpperCase()).join(''),
        s.split('').map((letter, i) => i % 2 ? letter.toUpperCase() : letter).join('')
      ];
    };
    ```

  </details>

  <details>
    <summary>
      ✔️ Sort the odd
    </summary>

    Description:  
    You have an array of numbers.
    Your task is to sort ascending odd numbers but even numbers must be on their places.

    Zero isn't an odd number and you don't need to move it. If you have an empty array, you need to return it.

    Example
    ```
    sortArray([5, 3, 2, 8, 1, 4]) == [1, 3, 2, 8, 5, 4]
    ```
    Solution:  
    ```javascript
    function sortArray(array) {
      const oddNumbers = array.filter(num => num % 2).sort((a, b) => a - b);
      let oddIndex = 0;
      return array.map(num => {
        if (num % 2) {
          oddIndex++
          return oddNumbers[oddIndex - 1]
        } else {
          return num
        }
      })
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Format a string of names like "Bart, Lisa & Maggie"
    </summary>

    Description:  
    Given: an array containing hashes of names

    Return: a string formatted as a list of names separated by commas except for the last two names, which should be separated by an ampersand.

    Example:
    ```
    list([ {name: 'Bart'}, {name: 'Lisa'}, {name: 'Maggie'} ])
    // returns 'Bart, Lisa & Maggie'

    list([ {name: 'Bart'}, {name: 'Lisa'} ])
    // returns 'Bart & Lisa'

    list([ {name: 'Bart'} ])
    // returns 'Bart'

    list([])
    // returns ''
    ```
    Note: all the hashes are pre-validated and will only contain A-Z, a-z, '-' and '.'.

    Solution:  
    ```javascript
    function list(names) {
      return names.reduce((res, elem, i) => res = `${res}${i === 0 ? '' : i === names.length - 1 ? ' & ' : ', '}${elem.name}`, '')
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Proof Read
    </summary>

    Description:  
    You've just finished writing the last chapter for your novel when a virus suddenly infects your document. It has swapped the 'i's and 'e's in 'ei' words and capitalised random letters. Write a function which will:

    a) remove the spelling errors in 'ei' words. (Example of 'ei' words: their, caffeine, deceive, weight)

    b) only capitalise the first letter of each sentence. Make sure the rest of the sentence is in lower case.

    Example: He haD iEght ShOTs of CAffIEne. --> He had eight shots of caffeine.

    Solution:  
    ```javascript
    function proofread(str) {
      return str.toLowerCase().replace(/ie/ig, 'ei').replace(/(^|[!?.]\s+)([a-z])/g, (m, g1, g2) => g1 + g2.toUpperCase());
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Simple Fun #79: Delete a Digit
    </summary>

    Description:  
    Task  
    Given an integer `n`, find the maximal number you can obtain by deleting exactly one digit of the given number.

    Example
    For `n = 152`, the output should be `52`;

    For `n = 1001`, the output should be `101`.

    Input/Output
    `[input]` integer `n`

    Constraints: `10 ≤ n ≤ 1000000`.

    `[output]` an integer

    Solution:  
    ```javascript
    function deleteDigit(n) {
      return Math.max(...[...String(n)].map((el, i, arr) => Number(arr.filter((dig, index) => index !== i).join(''))));
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Equal Sides Of An Array
    </summary>

    Description:  
    You are going to be given an array of integers. Your job is to take that array and find an index N where the sum of the integers to the left of N is equal to the sum of the integers to the right of N. If there is no index that would make this happen, return `-1`.

    For example:

    Let's say you are given the array `{1,2,3,4,3,2,1}`: Your function will return the index 3, because at the 3rd position of the array, the sum of left side of the index (`{1,2,3}`) and the sum of the right side of the index (`{3,2,1}`) both equal `6`.

    Let's look at another one.
    You are given the array `{1,100,50,-51,1,1}`: Your function will return the index `1`, because at the 1st position of the array, the sum of left side of the index (`{1}`) and the sum of the right side of the index (`{50,-51,1,1}`) both equal `1`.

    Last one:  
    You are given the array `{20,10,-80,10,10,15,35}`
    At index 0 the left side is `{}`
    The right side is `{10,-80,10,10,15,35}`
    They both are equal to `0` when added. (Empty arrays are equal to 0 in this problem)
    Index 0 is the place where the left side and right side are equal.

    Note: Please remember that in most programming/scripting languages the index of an array starts at 0.

    Input:  
    An integer array of length `0 < arr < 1000`. The numbers in the array can be any integer positive or negative.

    Output:  
    The lowest index `N` where the side to the left of `N` is equal to the side to the right of `N`. If you do not find an index that fits these rules, then you will return `-1`.

    Note:  
    If you are given an array with multiple answers, return the lowest correct index.

    Solution:  
    ```javascript
    function findEvenIndex(arr) {
      const arrSum = (array) => array.reduce((sum, el) => sum + el, 0)
      return arr.findIndex((el, i, arr) => arrSum(arr.slice(0, i)) === arrSum(arr.slice(i + 1)))
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Easy Balance Checking
    </summary>

    Description:  
    You are given a (small) check book as a - sometimes - cluttered (by non-alphanumeric characters) string:

    ```
    "1000.00
    125 Market 125.45
    126 Hardware 34.95
    127 Video 7.45
    128 Book 14.32
    129 Gasoline 16.10"
    The first line shows the original balance. Each other line (when not blank) gives information: check number, category, check amount.
    ```
    First you have to clean the lines keeping only letters, digits, dots and spaces.

    Then return a report as a string (underscores show spaces -- don't put them in your solution. They are there so you can see them and how many of them you need to have):
    ```
    "Original_Balance:_1000.00
    125_Market_125.45_Balance_874.55
    126_Hardware_34.95_Balance_839.60
    127_Video_7.45_Balance_832.15
    128_Book_14.32_Balance_817.83
    129_Gasoline_16.10_Balance_801.73
    Total_expense__198.27
    Average_expense__39.65"
    On each line of the report you have to add the new balance and then in the last two lines the total expense and the average expense. So as not to have a too long result string we don't ask for a properly formatted result.
    ```
    Notes  
    - It may happen that one (or more) line(s) is (are) blank.
    - Round to 2 decimals your results.
    - The line separator of results may depend on the language `\n` or `\r\n`. See examples in the "Sample tests".
    - R language: Don't use R's base function "mean()" that could give results slightly different from expected ones.

    Solution:  
    ```javascript
    function balance(book) {
      const normNum = (str) => Number(str).toFixed(2);
      return book
        .replace(/[^\w|^\.|^\s]/g, '')
        .split('\n')
        .filter(el => el.length > 0)
        .reduce((dataObj, el, i, arr) => {
          if (i === 0) {
            dataObj.text = `Original Balance: ${el}\r\n`;
            dataObj.originalBalance = normNum(el);
            dataObj.currentBalance = normNum(el);
          } else {
            const rowAsArr = el.split(' ');
            rowAsArr[2] = normNum(rowAsArr[2]);
            dataObj.currentBalance = normNum(dataObj.currentBalance - rowAsArr[2]);
            dataObj.text += `${rowAsArr.join(' ')} Balance ${dataObj.currentBalance}\r\n`;
            if (i === arr.length - 1) {
              dataObj.text += `Total expense  ${normNum(dataObj.originalBalance - dataObj.currentBalance)}\r\n`;
              dataObj.text += `Average expense  ${normNum((dataObj.originalBalance - dataObj.currentBalance) / (arr.length - 1))}`;
            }
          }
          return dataObj;
        }, {}).text;
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Sort with a sorting array
    </summary>

    Description:  
    Sort an array according to the indices in another array. It is guaranteed that the two arrays have the same size, and that the sorting array has all the required indices.

    initialArray = ['x', 'y', 'z'] sortingArray = [ 1, 2, 0]

    sort(initialArray, sortingArray) => ['z', 'x', 'y']

    sort(['z', 'x', 'y'], [0, 2, 1]) => ['z', 'y', 'x']

    Solution:  
    ```javascript
    function sort(initialArray, sortingArray) {
      return initialArray.reduce((arr, el, i) => {
        arr[sortingArray[i]] = initialArray[i];
        return arr;
      }, []);
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Zero-plentiful Array
    </summary>

    Description:  
    An array is called zero-plentiful if it contains at least one 0 and every sequence of 0s is of length at least 4. Your task is to return the number of zero sequences if the given array is zero-plentiful else 0.

    Solution:  
    ```javascript
    function zeroPlentiful(arr) {
      const strSeqs = arr.join('').match(/0+/g);
      if (strSeqs && Math.min(...strSeqs.map(el => el.length)) >= 4) {
        return strSeqs.length;
      } else {
        return 0;
      }
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ RGB To Hex Conversion
    </summary>

    Description:  
    The rgb function is incomplete. Complete it so that passing in RGB decimal values will result in a hexadecimal representation being returned. Valid decimal values for RGB are 0 - 255. Any values that fall out of that range must be rounded to the closest valid value.

    Note: Your answer should always be 6 characters long, the shorthand with 3 will not work here.

    The following are examples of expected output values:
    ```
    rgb(255, 255, 255) // returns FFFFFF
    rgb(255, 255, 300) // returns FFFFFF
    rgb(0,0,0) // returns 000000
    rgb(148, 0, 211) // returns 9400D3
    ```

    Solution:  
    ```javascript
    function rgb(r, g, b){
      return [r,g,b].map(el => ('00' + Math.min(Math.max(el, 0), 255).toString(16)).slice(-2)).join('').toUpperCase()
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Birthday I - Cake
    </summary>

    Description:  
    It's your Birthday. Your colleagues buy you a cake. The numbers of candles on the cake is provided (x). Please note this is not reality, and your age can be anywhere up to 1,000. Yes, you would look a mess.

    As a surprise, your colleagues have arranged for your friend to hide inside the cake and burst out. They pretend this is for your benefit, but likely it is just because they want to see you fall over covered in cake. Sounds fun!

    When your friend jumps out of the cake, he/she will knock some of the candles to the floor. If the number of candles that fall is higher than 70% of total candles (x), the carpet will catch fire.

    You will work out the number of candles that will fall from the provided string (y). You must add up the character ASCII code of each even indexed (assume a 0 based indexing) character in y, with the alphabetical position of each odd indexed character in y to give the string a total.

    example: 'abc' --> a=97, b=2, c=99 --> y total = 198.

    If the carpet catches fire, return 'Fire!', if not, return 'That was close!'.

    Solution:  
    ```javascript
    function cake(x, y) {
      return y
        .split('')
        .reduce((sum, el, i) => sum + el.charCodeAt(0) + (i % 2 ? -96 : 0), sum = 0) > (x * 0.7).toFixed(0) ? 'Fire!' : 'That was close!'
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Alphabetized
    </summary>

    Description:  
    The alphabetized kata  
    Re-order the characters of a string, so that they are concatenated into a new string in "case-insensitively-alphabetical-order-of-appearance" order. Whitespace and punctuation shall simply be removed!

    The input is restricted to contain no numerals and only words containing the english alphabet letters.

    Example:
    ```
    alphabetized("The Holy Bible") // "BbeehHilloTy"
    ```

    Solution:  
    ```javascript
    function alphabetized(s) {
      function charSorting(a, b) {
        if (a[0].toUpperCase() > b[0].toUpperCase()) return 1;
        if (a[0].toUpperCase() < b[0].toUpperCase()) return -1;
        return a[1] - b[1]
      }
      return s
        .replace(/[^a-zA-Z]+/g, '')
        .split('')
        .map((el, i) => [el, i])
        .sort(charSorting)
        .map(el => el[0])
        .join('')
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Smallest value of an array
    </summary>

    Description:  
    Write a function that can return the smallest value of an array or the index of that value. The function's 2nd parameter will tell whether it should return the value or the index.

    Assume the first parameter will always be an array filled with at least 1 number and no duplicates. Assume the second parameter will be a string holding one of two values: 'value' and 'index'.
    ```
    min([1,2,3,4,5], 'value') // => 1
    min([1,2,3,4,5], 'index') // => 0
    ```

    Solution:  
    ```javascript
    function min(arr, toReturn) {
      const minValue = Math.min(...arr);
      return toReturn === 'value' ? minValue : arr.indexOf(minValue)
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Element equals its index
    </summary>

    Description:  
    Given a sorted array of distinct integers, write a function `indexEqualsValue` that returns the lowest index for which `array[index] == index`. Return `-1` if there is no such index.

    Your algorithm should be very performant.

    [input] array of integers ( with 0-based nonnegative indexing )
    [output] integer

    Examples:
    ```
    input: [-8,0,2,5]
    output: 2 # since array[2] == 2

    input: [-1,0,3,6]
    output: -1 # since no index in array satisfies array[index] == index
    ```
    Random Tests Constraints:
    Array length: 200 000

    Amount of tests: 1 000

    Time limit: 150 ms

    Solution:  
    ```javascript
    function indexEqualsValue(a) {
      let start = 0;
      let end = a.length - 1;
      while (start != end) {
        let midEl = midElement();
        if (a[midEl] > midEl) {
          end = midEl - 1;
        } else if (a[midEl] < midEl) {
          start = midEl;
        } else {
          while (a[midEl] == midEl) {
            midEl--;
          }
          return midEl + 1;
        }
      }
      if (a[midElement()] == midElement()) {
        return midElement()
      }
      return -1;

      function midElement() {
        return Math.round((start + end) / 2);
      }
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Sort by Last Char
    </summary>

    Description:  
    Given a string of words (x), you need to return an array of the words, sorted alphabetically by the final character in each.

    If two words have the same last letter, they returned array should show them in the order they appeared in the given string.

    All inputs will be valid.

    Solution:  
    ```javascript
    function last(x) {
      return x.split(' ').sort((a, b) => a[a.length - 1] > b[b.length - 1] ? 1 : -1)
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ Sort array by string length
    </summary>

    Description:  
    Write a function that takes an array of strings as an argument and returns a sorted array containing the same strings, ordered from shortest to longest.

    For example, if this array were passed as an argument:

    `["Telescopes", "Glasses", "Eyes", "Monocles"]`

    Your function would return the following array:

    `["Eyes", "Glasses", "Monocles", "Telescopes"]`

    All of the strings in the array passed to your function will be different lengths, so you will not have to decide how to order multiple strings of the same length.

    Solution:  
    ```javascript
    function sortByLength(array) {
      return array.sort((a, b) => a.length - b.length);
    };
    ```

  </details>

  <details>
    <summary>
      ✔️ Binary Search
    </summary>

    Description:  
    A binary search algorithm is a way to look for the index of a certain value in a sorted array.

    The algorithm will progressively cut the original array into smaller and smaller chunks until it finds the desired value. If the desired value is not found, return -1.

    Let's take a look at an illustration from Wikipedia:

    > The list to be searched: L = 1 3 4 6 8 9 11. The value to be found: X = 4.

    > Compare X to 6. X is smaller. Repeat with L = 1 3 4.

    > Compare X to 3. X is bigger. Repeat with L = 4.

    > Compare X to 4. They are equal. We're done, we found X.

    [More information on Wikipedia](http://en.wikipedia.org/wiki/Binary_search_algorithm)

    This makes it efficient for particularly large arrays because it doesn't have to completely iterate over them, so it will only take logarithmic time.

    Write a function binSearch that can perform a binary search on large arrays and not time out. The function will have 2 parameters, which are a sorted array and an element to search.

    Note: indexOf, lastIndexOf, eval, sort and sortedIndex are disabled.

    Solution:  
    ```javascript
    function binSearch(arr, toSearch) {
      let start = 0;
      let end = arr.length - 1;
      while (start != end) {
        let midEl = midElement();
        if (arr[midEl] > toSearch) {
          end = midEl - 1;
        } else if (arr[midEl] < toSearch) {
          start = midEl;
        } else {
          while (arr[midEl] == toSearch) {
            midEl--;
          }
          return midEl + 1;
        }
      }
      if (arr[midElement()] == midElement()) {
        return midElement()
      }
      return -1;

      function midElement() {
        return Math.round((start + end) / 2);
      }
    }
    ```

  </details>

  <details>
    <summary>
      ✔️ I love big nums and I cannot lie
    </summary>

    Description:  
    Write

    ```
    function biggest(nums)
    ```
    that given an array of numbers >= 0, will arrange them such that they form the biggest number.

    For example:
    ```
    biggest([1, 2, 3]) === '321'
    biggest([3, 30, 34, 5, 9]) === '9534330'
    ```
    The results will be large so make sure to return a string.

    Solution:  
    ```javascript
    function biggest(nums) {
      return nums
      .sort((a, b) => [a, b].join('') > [b, a].join('') ? -1 : 1)
      .join('')
      .replace(/(^0*)(?=.$)/, '');
    };
    ```

  </details>

</details>

* <details>
  <summary>
    ✔️ Способы сделать из объекта массив.
  </summary>

  The easiest way to make `array` from `object` is `Object.entries()` method
  
  ```javascript
  const someObject = {a:1, b:2, c:'sometext'};
  const arrayFromObject = Object.entries(someObject);
  console.log(arrayFromObject);
  ```
  Also there are options to make it via `Object.keys()` or `Object.values()`


</details>

* <details>
  <summary>
    ✔️ Реализовать любую функцию из перебирающих методов: например map, reduce, filter, чтобы она вызывалась у массивов как и полагается: arr.reduce, arr.filter.
  </summary>

  ```javascript
  const arr = [0,1,2,3,4,5,6,7,8,9]

  arrQuadrupled = arr.map(elem => elem*4);
  arrSummarized = arr.reduce((sum, elem) => elem += sum, 0);
  arrEvenOnly = arr.filter(elem => elem % 2 === 0);

  console.log(`Initial array: ${arr.toString()}`)
  console.log(`Qudrupled array: ${arrQuadrupled.toString()}`)
  console.log(`Sum of array: ${arrSummarized.toString()}`)
  console.log(`Filtered array(even only): ${arrEvenOnly.toString()}`)
  ```

</details>

 
* ❌ Ассинхронность в JS, с помощью чего достигается? Стек вызовов, Web Api, Event Loop, очередь колбеков.
* ❌ Таймеры в JS. Отличие setInterval от рекурсивного setTimeout.
* ❌ Как поведёт себя SetTimeout на ноль секунд?
* ❌ Что такое промис? Реализовать функцию задержку.
* ❌ Что быстрее выполнится, setTimeout или промис, почему?
* ❌ Map и Set.
* ❌ Формат JSON, методы JSON.
* ❌ Отправка запросов, какие есть способы и разница?
* ❌ localStorage и sessionStorage.

---

Работа с Dom:

* ❌ В чем отличие document.getElement... методов, от document.querySelector методов. В каких случаях стоит использовать первые, а в каких вторые? Какие работают быстрее?
* ❌ Как отменить действия при событии по умолчанию?
* ❌ Добавление, создание и удаление элементов из DOM.
* ❌ el.textContent vs el.innerHTML
* ❌ Всплытие событий и погружение.
* ❌ Делегирование событий.

---

Прочее:

* ❌ Сложность алгоритмов.
* ❌ Что такое npm, yarn? Как прописывать npm скрипты?
* ❌ Регулярные выражения.