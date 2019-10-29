# JS 

## operator spread
```
[a, b, ...iterableObj] = [1, 2, 3, 4, 5]; // iterableObj -> [3, 4, 5]
```

## Hoisting
```javascript
var a = 5;  
function foo() {  
  console.log(a); // undefined  
  var a = 10;  
}  
foo();

say('user'); // undefined, user
var phrase = 'Hello';
function say(name) {
  console.log( `${phrase}, ${name}` );
}

var foo = 1; 
function bar() { 
    if (!foo) { 
        var foo = 10; 
    } 
    console.log(foo); // 10
} 
bar();

var a = 1; 
function b() { 
    a = 10; 
    return; 
    function a() {} 
} 
b();
console.log(a); // 1
```

## Closures
```
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i); // 10 10
  },0);
}

for (let i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i); // from 0 to 9
  },0);
}

for (var i = 0; i < 10; i++) {
  (function(i){
    setTimeout(function() {
      console.log(i); // from 0 to 9
    },0);
  }(i));
}


var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var Counter1 = makeCounter();
var Counter2 = makeCounter();

Counter1.increment();
Counter1.increment();
console.log(Counter1.value()); //2

console.log(Counter2.value()); //0
```

## Currying
```
var sum = function (a) {
  return function(b) {
    return a + b;
  }
}
sum(5)(6); // 11

// Or
const sum = a => b => a + b;
sum(5)(6); // 11

```

## Typing
```
var a = '5' + 1; // "51"
var a = '5' - 1; // 4

6 / "3" // 2

"2" * "3" // 6

4 + 5 + "px" // "9px"

"$" + 4 + 5 // "$45"

"4" - 2 // 2

"4px" - 2 // NaN
 
7 / 0 // Infinity

typeof null // "object"

typeof {}[0] // "undefined"

typeof ("4px" - 2) // "number"

parseInt("09") // 9

5 && 2 // 2
2 && 5 // 5
1 && 0 // 0
0 && -1 // 0
0 && 1 // 0

5 || 0 // 5
0 || 5 // 5
0 || -1 // -1
-1 || 0 // -1
```

## [native code]
```
function baz() {
  var baz = b = 5;
}
baz();
console.log(baz); // ƒ baz() { var baz = b = 5; }
console.log(b); // 5
```

## Strict mode
```
'use strict';
var f = function () {
  console.log('1'); // (2) '1'
}

(function() {
  console.log('2'); // (1) '2'
}())


'use strict';
NaN = 5; // TypeError

'use strict';
myVar = 12; // ReferenceError

'use strict';
0644 === 420 // SyntaxError: Octal literals are not allowed in strict mode.

'use strict';
var x;
delete x; // SyntaxError

```

## Fibonacci
```
function fib(n) {
  let a = 1, b =1;

  for (let i = 3; i <= n; i++) {
    let c = a+b;
    a = b;
    b = c;
  };
  return b;
}
console.log(fib(7)); // 13
```

## Factorial
```
function fac(n) {
  return n ? n * fac(n - 1) : 1;
}
console.log(fac(5)); // 120
```

##
```
let sortBubble = (arr) => {
  let tmp, c = 0;

  for (let i = arr.length - 1; i > 0; i--) {
    for (let j = 0; j < i; j++) {

      if (arr[j] > arr[j+1]) {
        tmp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = tmp;
        c++;
      }

    }

    if (c === 0) {
        break;
    }
  };

  return arr;
}
sortBubble( [5, 20, 3, 11, 1, 17, 3, 12, 8, 10, 22]); // [1, 3, 3, 5, 8, 10, 11, 12, 17, 20, 22]


let a = [1, 12, 5, 26, 7, 14, 3, 7, 2, 3];

function quickSort( arr, left, right) {
    let index = partition(arr, left, right);
    if (left < index - 1)
        quickSort(arr, left, index - 1);
    if (index < right)
        quickSort(arr, index, right);
}

function partition(arr, left, right) {
    let pivot = arr[Math.floor((left + right) / 2)]
      , i = left
      , j = right
      , tmp;

    while (i <= j) {
        while (arr[i] < pivot)
            i++;
        while (arr[j] > pivot)
            j--;
        if (i <= j) {
            tmp = arr[i];
            arr[i] = arr[j];
            arr[j] = tmp;
            i++;
            j--;
        }
    }
    return i;
}
quickSort(a, 0, a.length-1);
console.log(a);


let getMaxNumber = function(arr) {
    let min = arr[0]
    ,   max = min;

    for(let i = 0, l = arr.length; i < l; i++) {
        if(arr[i] > max) max = arr[i];
        if(arr[i] < min) min = arr[i];
    }
    return max;
};
console.log(getMaxNumber([2,4,55,67,9,0,6]));


let i = 10, array = [];

while (i--) {
  array.push(function() {
    return i + i;
  });
}
console.log( [array[0](), array[1]()] ); // [-2,-2]


let A, B;
A = B = 'test';
A.c = 1;
B.c = 2;
console.log(A.c); // undefined
console.log(B.c); // undefined


let f = function() { 
  console.log(this.x);
};
let obj = {x: 'test'};

f.prototype = obj;
new f(); // "test"
```

## Descriptors
```
некоторые флаги:

    * writable — значение свойства может быть изменено, используется только для дескрипторов данных.
    * configurable — тип свойства может быть изменён или свойство может быть удалено.
    * enumerable — свойство используется в общем перечислении.
      Дескрипторы данных таковы, что определяют конкретное значение, которое соответствует дополнительному
      value - параметру, описывающему конкретные данные, привязанные к свойству:
    * value — значение свойства
```

## Напишите функцию принимающую строку с именем файла и возвращающую его расширение
```
'some.class.js'.split('.').pop(); // "js"
```

## Привязка контекста (Bind, Call, Apply)
```
Методы call/apply вызывают функцию с заданным контекстом и аргументами.

А bind не вызывает функцию. Он только возвращает «обёртку», которую мы можем вызвать позже, и которая передаст вызов в исходную функцию, с привязанным контекстом.

function bind(func, context) {
  return function() {
    return func.apply(context, arguments);
  };
}

var user = {
  firstName: "Vasili",
  sayHi: function() {
    console.log( this.firstName );
  }
};

setTimeout(bind(user.sayHi, user), 100);
```

## Структуры данных
```
/*** ===================================================================== ***\
 *           a           b                                 d                 *
 *           a         b    O(N^2)                      d                    *
 *     O(N!) a        b                O(N log N)    d                    c  *
 *           a      b                            d                 c         *
 *          a      b                          d             c        O(N)    *
 *          a    b                         d         c                       *
 *          a  b                       d      c                              *
 *         a  b                     d  c                                     *
 *         ab                   c                          O(1)              *
 *  e    e    e    e    ec   d    e    e    e    e    e     e    e    e      *
 *      ba        c      d                                                   *
 *    ba   c        d                       f    f    f    f    f    f    f  *
 ** cadf    f d    f    f    f    f    f       O(log N)                     **
\*** ===================================================================== ***/

«О» большое — обозначение способа приблизительной оценки производительности алгоритмов для относительного сравнения.

                          Доступ      Поиск       Вставка      Удаление
------------------------------------------------------------------------
                Массив    O(1)        O(N)        O(N)         O(N)
        Связный список    O(N)        O(N)        O(1)         O(1)
Двоичное дерево поиска    O(log N)    O(log N)    O(log N)     O(log N)

                          Доступ       Поиск      Вставка      Удаление
------------------------------------------------------------------------
                Массив    ОХРЕНЕННО    НОРМАС     НОРМАС       НОРМАС
        Связный список    НОРМАС       НОРМАС     ОХРЕНЕННО    ОХРЕНЕННО
Двоичное дерево поиска    КРУТО        КРУТО      КРУТО        КРУТО
```

**Список** — представление пронумерованной последовательности значений, где одно и то же значение может присутствовать сколько угодно раз.
```
Списки отлично справляются с быстрым доступом к элементам в своём конце и работой с ними.
Но для элементов из начала или середины они не слишком хороши, так как приходится вручную обрабатывать адреса памяти.
```
Сложность операции доступа в список — O(1)  
Удаление элемента из конца списка — O(1)  
Добавление элемента в начало списка — линейно O(N)  
Удаление элемента из начала списка — линейно O(N)  

**Хеш-таблица** — неупорядоченная структура данных. Вместо индексов мы работаем с «ключами» и «значениями», вычисляя адрес памяти по ключу.

Сложность чтения значения из хеш-таблицы — константа O(1)  
Сложность установки значения в хеш-таблицу — константа O(1)  
Сложность удаления значения из хеш-таблицы — константа O(1)  

**Стеки** похожи на списки. Они также упорядочены, но ограничены в действиях: можно лишь добавлять и убирать значения из конца списка. 
















