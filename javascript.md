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
    ❌ Методы массивов. (Задачки)
  </summary>

  ???

</details>

* <details>
  <summary>
    ❌ Способы сделать из объекта массив.
  </summary>

  ???

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