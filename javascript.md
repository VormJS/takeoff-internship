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
    ⏳ Методы массивов. (Задачки)
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
      ✔️ 
    </summary>

    Description:  
    

    Solution:  
    ```javascript
    
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