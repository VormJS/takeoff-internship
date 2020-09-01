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

  typeof NaN - "number"  
  typeof Null - "object", but it's language mistake
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
  uses sctrict comparsion, different types returns false

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

  null - empty value  
  undefined - declared and not assigned variable
</details>

* <details>
  <summary>
    ✔️ В чем разница между переменными, созданными с помощью let, var или const? Хоистинг переменных.
  </summary>

  let and const may be used inside curved brackets {} where they declared and initialized (ReferenceError otherwise).
  let variable can be reassigned, const variable can not be reassigned.  
  var have weird and hardly controlled behaviour, better don't use it.  

  Hoisting moves variable declarations to the top of code. That makes possible to use variables before declaration. But hoisting does not working for initializing. Also hoisting does not working for let and const.  

  As good rule: **always declare all variables at the beginning of every scope.**

  strict mode blocks opportunity to use variable before declaration.

</details>

* ❌ Use strict. Что это? Приведите пример разного поведения строго режима и обычного.
* ❌ Виды функций. Отличие стрелочных функций. Что такое и в чем разница между Function Expression и Function Declaration?
* ❌ Что такое this? Методы привязки контекста и их различие?
* ❌ Замыкания. Что это такое? Задачки: написать функцию которая работает таким образом: multiply(7)(3)(2) => 42.
* ❌ Прототипы, прототипное наследование. Перебираем обьект, как определить чье поле, обьекта или прототипа? Написать функцию, которая отработает следующим образом: 4.plus(2).minus(1) => 5
---
* ❌ typeof([]). Как отличить массив от обьекта?
* ❌ Как скопировать обьект в другой обьект? Передача по ссылке. Написать функцию которая работает как Object.assign, которая скопирует поля обьекта в другой обьект с любой вложенностью.
* ❌ Методы массивов. (Задачки)
* ❌ Способы сделать из объекта массив.
* ❌ Реализовать любую функцию из перебирающих методов: например map, reduce, filter, чтобы она вызывалась у массивов как и полагается: arr.reduce, arr.filter.
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