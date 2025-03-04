JavaScript
Основы JavaScript
JavaScript – это язык программирования, используемый для создания интерактивных веб-приложений. Он поддерживает работу с браузером, серверную разработку (Node.js) и мобильные приложения.
Что такое JavaScript и где он используется?
JavaScript – это язык программирования, который изначально использовался для динамического изменения веб-страниц в браузерах. Сейчас он применяется не только в браузере, но и на сервере (Node.js), в мобильных приложениях и даже в разработке игр.

// Вывод в консоль
console.log('Привет, мир!');

// Функция, изменяющая текст на странице
document.getElementById('demo').innerText = 'Новый текст';

В чем разница между var, let и const?
- `var` – имеет функциональную область видимости, подвержен `hoisting`.
- `let` – имеет блочную область видимости, не подвержен `hoisting`.
- `const` – аналогичен `let`, но значение нельзя переназначить.

var name = 'Alice';
let age = 25;
const city = 'Moscow';

name = 'Bob'; // Можно переопределить
age = 30; // Можно изменить
city = 'Saint Petersburg'; // Ошибка, нельзя изменить const

Что такое hoisting?
Hoisting (поднятие) – это механизм JavaScript, при котором объявления переменных и функций перемещаются в начало их области видимости перед выполнением кода.

console.log(name); // undefined (из-за hoisting)
var name = 'Alice';

// Для let и const hoisting не работает:
console.log(age); // ReferenceError
let age = 25;

Как работает приведение типов в JavaScript?
JavaScript автоматически преобразует типы данных в зависимости от операции. Приведение может быть явным (`Number(value)`, `String(value)`) или неявным (`'5' + 5 = '55'`).

console.log('5' + 5); // '55' (строка)
console.log('5' - 5); // 0 (число)
console.log(Boolean(0)); // false

Чем отличается == от ===?
`==` сравнивает значения с приведением типов, а `===` сравнивает значения без преобразования.

console.log(5 == '5'); // true (приведение типов)
console.log(5 === '5'); // false (разные типы)

Что такое замыкание (closure)?
Замыкание – это функция, которая запоминает переменные из внешней области видимости, даже после завершения её выполнения.

function createCounter() {
    let count = 0;
    return function() {
        count++;
        return count;
    };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2

Что такое TDZ (Temporal Dead Zone)?
TDZ – это временная область, в которой переменная объявлена, но к ней нельзя обратиться до момента её инициализации.

console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 10;

Основы JavaScript включают в себя работу с переменными, область видимости, приведение типов, замыкания и многие другие механики, которые являются ключевыми для понимания языка.
 
Функции и область видимости в JavaScript
Функции являются основным строительным блоком программ на JavaScript. Они могут быть объявлены разными способами и имеют разную область видимости.
Как работает область видимости в JavaScript?
JavaScript поддерживает три типа области видимости:
- **Глобальная область видимости** – переменные доступны везде.
- **Функциональная область видимости** – переменные доступны только внутри функции.
- **Блочная область видимости (let, const)** – переменные доступны только внутри блока `{}`.

var globalVar = "Я глобальная переменная";

function testScope() {
    var localVar = "Я внутри функции";
    console.log(globalVar); // Доступна
    console.log(localVar);  // Доступна
}

testScope();
console.log(localVar); // Ошибка, переменная недоступна

Что такое callback-функция?
Callback-функция – это функция, передаваемая в другую функцию в качестве аргумента и вызываемая внутри неё.

function greeting(name, callback) {
    console.log("Привет, " + name);
    callback();
}

function sayBye() {
    console.log("Пока!");
}

greeting("Алиса", sayBye);

В чем разница между function declaration, function expression и arrow function?
- **Function Declaration** – объявляется именованной и доступна в любом месте кода благодаря hoisting.
- **Function Expression** – объявляется внутри переменной, не подвержена hoisting.
- **Arrow Function** – краткая запись функции, не имеет собственного `this`.

// Function Declaration
function sayHello() {
    console.log("Hello!");
}

// Function Expression
const sayHelloExpr = function() {
    console.log("Hello!");
};

// Arrow Function
const sayHelloArrow = () => console.log("Hello!");

Как работает this в JavaScript?
`this` ведёт себя по-разному в зависимости от контекста:
- В глобальном контексте `this` ссылается на `window` (в браузере) или `global` (в Node.js).
- В методах объектов `this` указывает на сам объект.
- В стрелочных функциях `this` сохраняет контекст родительской функции.

// Глобальный контекст
console.log(this); // window или global

// Внутри объекта
const obj = {
    name: "Alice",
    greet() {
        console.log(this.name);
    }
};
obj.greet(); // Alice

// В стрелочной функции
const obj2 = {
    name: "Bob",
    greet: () => {
        console.log(this.name); // undefined, т.к. this берётся из внешнего контекста (window)
    }
};
obj2.greet();

Как изменить контекст this? (call, apply, bind)
Методы `call`, `apply` и `bind` позволяют явно задавать `this`.

function introduce(greeting) {
    console.log(greeting + ", меня зовут " + this.name);
}

const user = { name: "Анна" };

introduce.call(user, "Привет"); // Привет, меня зовут Анна
introduce.apply(user, ["Здравствуйте"]); // Здравствуйте, меня зовут Анна

const boundFunc = introduce.bind(user);
boundFunc("Привет"); // Привет, меня зовут Анна

Как передавать параметры по умолчанию в функции?
В ES6+ можно задавать параметры по умолчанию прямо в объявлении функции.

function greet(name = "Гость") {
    console.log("Привет, " + name);
}

greet(); // Привет, Гость
greet("Алиса"); // Привет, Алиса

Функции – важный компонент JavaScript. Понимание их работы, области видимости и особенностей `this` помогает писать более чистый и предсказуемый код.
 
Объекты и прототипы в JavaScript
Объекты являются ключевой структурой данных в JavaScript. Они используются для хранения информации в виде пар «ключ-значение». JavaScript также поддерживает прототипное наследование, позволяя объектам наследовать свойства друг от друга.
Как создать объект в JavaScript?
Объект можно создать несколькими способами:

// Создание объекта через литерал
const person = {
    name: "Alice",
    age: 25,
    greet() {
        console.log("Привет, меня зовут " + this.name);
    }
};

// Создание объекта через конструктор
const user = new Object();
user.name = "Bob";
user.age = 30;

// Создание объекта через Object.create()
const admin = Object.create(person);
admin.name = "Charlie";

В чем разница между Object.create() и new?
- `Object.create(proto)` создаёт объект с указанным прототипом.
- `new` используется с функцией-конструктором для создания объекта.

// Использование Object.create()
const baseUser = { role: "user" };
const user1 = Object.create(baseUser);
console.log(user1.role); // "user"

// Использование new
function User(name) {
    this.name = name;
}

const user2 = new User("Alice");
console.log(user2.name); // "Alice"

Что такое прототипное наследование?
JavaScript использует прототипное наследование – механизм, при котором объекты наследуют свойства и методы от других объектов через цепочку прототипов.

// Базовый объект
const animal = {
    speak() {
        console.log(this.name + " издает звук");
    }
};

// Создание объекта с наследованием
const dog = Object.create(animal);
dog.name = "Шарик";
dog.speak(); // "Шарик издает звук"

Как работает Object.assign() и spread-оператор?
- `Object.assign(target, source)` копирует свойства из `source` в `target`.
- Spread-оператор `...` делает то же самое, но в более удобной форме.

const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };

// Object.assign()
const merged1 = Object.assign({}, obj1, obj2);
console.log(merged1); // { a: 1, b: 3, c: 4 }

// Spread-оператор
const merged2 = { ...obj1, ...obj2 };
console.log(merged2); // { a: 1, b: 3, c: 4 }

Как работают геттеры и сеттеры (get/set)?
Геттеры (`get`) и сеттеры (`set`) позволяют управлять доступом к свойствам объекта.

const user = {
    firstName: "Alice",
    lastName: "Johnson",
    
    get fullName() {
        return this.firstName + " " + this.lastName;
    },
    
    set fullName(value) {
        [this.firstName, this.lastName] = value.split(" ");
    }
};

console.log(user.fullName); // "Alice Johnson"
user.fullName = "Bob Smith";
console.log(user.fullName); // "Bob Smith"

Объекты – ключевая часть JavaScript. Они используются для организации данных, а прототипное наследование позволяет эффективно управлять свойствами и методами.
 
Асинхронность в JavaScript
JavaScript работает в однопоточном режиме, но поддерживает асинхронные операции благодаря Event Loop, Callbacks, Promises и async/await.
Что такое Event Loop и как он работает?
Event Loop – это механизм в JavaScript, который позволяет выполнять асинхронные операции без блокировки основного потока выполнения. Он управляет очередями задач (macrotasks и microtasks).

console.log("Начало");

setTimeout(() => {
    console.log("Таймер 0 мс");
}, 0);

Promise.resolve().then(() => {
    console.log("Promise");
});

console.log("Конец");

// Вывод в консоли:
// Начало
// Конец
// Promise
// Таймер 0 мс

Как работают Promise и async/await?
`Promise` – это объект, представляющий результат асинхронной операции. `async/await` – синтаксический сахар для работы с Promise.

// Пример Promise
const fetchData = () => {
    return new Promise((resolve) => {
        setTimeout(() => resolve("Данные загружены"), 2000);
    });
};

fetchData().then(data => console.log(data));

// Пример async/await
async function getData() {
    const data = await fetchData();
    console.log(data);
}

getData();

Что такое Microtasks и Macrotasks?
JavaScript выполняет асинхронные задачи в двух очередях: Microtasks и Macrotasks.
- **Microtasks**: `Promise.then`, `MutationObserver`.
- **Macrotasks**: `setTimeout`, `setInterval`, `setImmediate`, `requestAnimationFrame`.

console.log("Начало");

setTimeout(() => console.log("setTimeout"), 0);
Promise.resolve().then(() => console.log("Promise"));

console.log("Конец");

// Вывод:
// Начало
// Конец
// Promise
// setTimeout

Чем setTimeout(fn, 0) отличается от Promise.resolve().then(fn)?
`setTimeout(fn, 0)` – это macrotask, выполняется после microtasks. `Promise.resolve().then(fn)` – это microtask, выполняется раньше macrotasks.
Как отловить ошибку в async/await?
Можно использовать `try/catch` или `.catch()` для обработки ошибок в асинхронных функциях.

async function fetchData() {
    try {
        let response = await fetch("https://example.com/data");
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Ошибка загрузки данных:", error);
    }
}

fetchData();

Асинхронность – важная часть JavaScript. Понимание Event Loop, Promises, async/await и очередей задач помогает эффективно работать с асинхронным кодом.
 
Работа с DOM и событиями в JavaScript
DOM (Document Object Model) – это структура документа, с которой можно взаимодействовать с помощью JavaScript. События позволяют реагировать на действия пользователя (клики, нажатия клавиш и т. д.).
Как получить элемент из DOM (querySelector, getElementById)?
JavaScript предоставляет несколько способов поиска элементов в DOM.

// Поиск по id
const elementById = document.getElementById("myId");

// Поиск по классу (возвращает HTMLCollection)
const elementsByClass = document.getElementsByClassName("myClass");

// Поиск по тегу (возвращает HTMLCollection)
const elementsByTag = document.getElementsByTagName("div");

// Современные методы поиска
const queryElement = document.querySelector(".myClass"); // Первый найденный элемент
const queryElements = document.querySelectorAll(".myClass"); // Все элементы с классом

Как добавить/удалить обработчик события?
Используйте `addEventListener` для добавления события и `removeEventListener` для удаления.

// Добавление обработчика клика
function handleClick() {
    console.log("Кнопка нажата!");
}

const button = document.getElementById("myButton");
button.addEventListener("click", handleClick);

// Удаление обработчика события
button.removeEventListener("click", handleClick);

В чем разница между event.target и event.currentTarget?
`event.target` – элемент, на котором произошло событие.
`event.currentTarget` – элемент, на котором висит обработчик.

document.getElementById("myDiv").addEventListener("click", function(event) {
    console.log("target:", event.target); // Элемент, по которому кликнули
    console.log("currentTarget:", event.currentTarget); // Элемент, на котором висит обработчик
});

Что такое Event Delegation?
Event Delegation – это техника, при которой обработчик вешается на родительский элемент, а события обрабатываются через `event.target`.

document.getElementById("parent").addEventListener("click", function(event) {
    if (event.target.classList.contains("child")) {
        console.log("Клик по дочернему элементу:", event.target.textContent);
    }
});

Как работает Capture и Bubbling?
События в JavaScript проходят через три стадии:
- **Capturing (перехват)** – событие идет сверху вниз (от `document` к элементу).
- **Target** – событие достигает целевого элемента.
- **Bubbling (всплытие)** – событие поднимается от элемента к `document`.

document.getElementById("outer").addEventListener("click", () => {
    console.log("Внешний элемент");
}, true); // Capture фаза

document.getElementById("inner").addEventListener("click", () => {
    console.log("Внутренний элемент");
}, false); // Bubbling фаза

// Если кликнуть на #inner, сначала сработает outer (capture), потом inner (bubbling)

Работа с DOM и событиями – важная часть разработки на JavaScript. Понимание событий, всплытия, делегирования и работы с элементами помогает создавать интерактивные веб-приложения.
 
ES6+ и современные возможности JavaScript
ES6 (ECMAScript 2015) и последующие версии добавили много новых возможностей, улучшив читаемость и производительность кода.
Что такое деструктуризация?
Деструктуризация позволяет извлекать значения из массивов и объектов в отдельные переменные.

// Деструктуризация массива
const [a, b] = [1, 2];
console.log(a, b); // 1, 2

// Деструктуризация объекта
const user = { name: "Alice", age: 25 };
const { name, age } = user;
console.log(name, age); // Alice, 25

Как работают Rest и Spread операторы?
- **Spread (`...`)** – разворачивает массив или объект.
- **Rest (`...`)** – собирает оставшиеся элементы в массив.

// Spread для объединения массивов
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];
console.log(arr2); // [1, 2, 3, 4, 5]

// Rest для передачи аргументов
function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
}
console.log(sum(1, 2, 3, 4)); // 10

Что такое WeakMap и WeakSet?
WeakMap и WeakSet – это коллекции, которые позволяют хранить слабые ссылки на объекты, что предотвращает утечки памяти.

const weakMap = new WeakMap();
let obj = { name: "Alice" };
weakMap.set(obj, "data");

obj = null; // Объект удаляется из памяти

const weakSet = new WeakSet();
let user = { id: 1 };
weakSet.add(user);

user = null; // Объект также удаляется

В чем разница между forEach, map, reduce?
- `forEach()` – выполняет функцию для каждого элемента массива, но не возвращает новый массив.
- `map()` – создает новый массив, преобразуя каждый элемент.
- `reduce()` – сводит массив к одному значению.

const numbers = [1, 2, 3, 4];

numbers.forEach(num => console.log(num * 2)); // Выводит: 2, 4, 6, 8

const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]

const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10

Как работают Set и Map?
- `Set` – коллекция уникальных значений.
- `Map` – коллекция пар ключ-значение, где ключ может быть любым типом данных.

// Пример Set
const uniqueNumbers = new Set([1, 2, 2, 3]);
console.log(uniqueNumbers); // Set {1, 2, 3}

// Пример Map
const userRoles = new Map();
userRoles.set("Alice", "Admin");
console.log(userRoles.get("Alice")); // Admin

Современные возможности JavaScript упрощают код и делают его более выразительным, позволяя писать более эффективные приложения.
 
Работа с сетью в JavaScript
JavaScript позволяет отправлять HTTP-запросы, работать с API и получать данные с серверов с помощью `fetch()`, `XMLHttpRequest`, WebSockets и других методов.
Как работает fetch()?
`fetch()` – это современный способ выполнения HTTP-запросов в JavaScript, он работает на промисах и поддерживает асинхронные операции.

fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error("Ошибка:", error));

Что такое CORS и как его обойти?
CORS (Cross-Origin Resource Sharing) – это механизм безопасности браузера, который предотвращает выполнение запросов с одного домена на другой.
Обойти CORS можно:
- Используя прокси-сервер.
- Включив CORS-заголовки на сервере.
- Используя JSONP (устаревший метод).
Чем XMLHttpRequest отличается от fetch?
`XMLHttpRequest` – устаревший метод для работы с HTTP-запросами, он поддерживает обработку состояний, но менее удобен по сравнению с `fetch()`.

const xhr = new XMLHttpRequest();
xhr.open("GET", "https://jsonplaceholder.typicode.com/posts/1");
xhr.onload = function() {
    if (xhr.status === 200) {
        console.log(JSON.parse(xhr.responseText));
    }
};
xhr.send();

Что такое WebSockets и как их использовать?
WebSockets позволяют устанавливать постоянное соединение между клиентом и сервером, что делает их удобными для чатов и стриминга данных.

const socket = new WebSocket("wss://example.com/socket");

socket.onopen = () => {
    console.log("Соединение установлено");
    socket.send("Привет, сервер!");
};

socket.onmessage = event => {
    console.log("Получено сообщение:", event.data);
};

socket.onclose = () => console.log("Соединение закрыто");

Как реализовать поллинг и long polling?
- **Обычный поллинг** – клиент отправляет запросы на сервер через интервалы времени.
- **Long polling** – клиент отправляет запрос и ждет ответа, а сервер отправляет ответ только при изменении данных.

// Обычный поллинг (запрос каждые 5 секунд)
setInterval(() => {
    fetch("https://example.com/data")
        .then(response => response.json())
        .then(data => console.log("Данные обновлены:", data));
}, 5000);

// Long polling (сервер отвечает при изменении данных)
function longPolling() {
    fetch("https://example.com/long-poll")
        .then(response => response.json())
        .then(data => {
            console.log("Новые данные:", data);
            longPolling(); // Повторный вызов
        })
        .catch(error => setTimeout(longPolling, 5000)); // Повтор при ошибке
}

longPolling();

JavaScript поддерживает различные способы взаимодействия с сетью, включая `fetch()`, WebSockets, CORS-защиту и механизмы поллинга для обновления данных.
 
Оптимизация и производительность в JavaScript
Оптимизация кода в JavaScript помогает ускорить выполнение скриптов, уменьшить нагрузку на браузер и сервер, а также улучшить пользовательский опыт.
Как уменьшить загрузку страницы?
Способы оптимизации загрузки страницы:
- Минимизация размера JavaScript и CSS файлов (`minification`).
- Использование **Lazy Loading** для изображений и ресурсов.
- Оптимизация запросов к серверу (кеширование, сжатие данных).
- Асинхронная загрузка скриптов (`async`, `defer`).

<!-- Асинхронная загрузка скрипта -->
<script async src="script.js"></script>

<!-- Отложенная загрузка (после анализа HTML) -->
<script defer src="script.js"></script>

Как работает Debounce и Throttle?
- **Debounce** – задерживает выполнение функции до окончания серии вызовов.
- **Throttle** – ограничивает выполнение функции с определенным интервалом.

// Debounce: запускает функцию только после паузы между вызовами
function debounce(func, delay) {
    let timeout;
    return function (...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), delay);
    };
}

// Throttle: ограничивает выполнение функции
function throttle(func, limit) {
    let lastCall = 0;
    return function (...args) {
        const now = Date.now();
        if (now - lastCall >= limit) {
            lastCall = now;
            func.apply(this, args);
        }
    };
}

Как использовать Memoization?
Memoization – это техника кэширования результатов функций для избежания повторных вычислений.

function memoize(fn) {
    const cache = {};
    return function (...args) {
        const key = JSON.stringify(args);
        if (!cache[key]) {
            cache[key] = fn.apply(this, args);
        }
        return cache[key];
    };
}

const slowFunction = num => {
    console.log("Вычисление...");
    return num * 2;
};

const fastFunction = memoize(slowFunction);

console.log(fastFunction(5)); // Вычисление...
console.log(fastFunction(5)); // Достается из кэша

Что такое Lazy Loading?
Lazy Loading (отложенная загрузка) – это техника, при которой ресурсы загружаются только тогда, когда они становятся видимыми.

<img src="placeholder.jpg" data-src="real-image.jpg" class="lazy">

<script>
document.addEventListener("DOMContentLoaded", function() {
    const lazyImages = document.querySelectorAll(".lazy");
    lazyImages.forEach(img => {
        img.src = img.dataset.src;
    });
});
</script>

Как работает requestAnimationFrame()?
`requestAnimationFrame()` позволяет оптимизировать анимации, синхронизируя их с частотой обновления экрана.

function animate() {
    console.log("Кадр анимации");
    requestAnimationFrame(animate);
}

requestAnimationFrame(animate);

Оптимизация JavaScript-кода помогает улучшить производительность веб-приложений, ускорить загрузку страниц и повысить отзывчивость интерфейса.
 
Безопасность в JavaScript
Безопасность в JavaScript – важный аспект разработки. Веб-приложения подвержены различным атакам, таким как XSS, CSRF, SQL-инъекции, и их нужно защищать на уровне фронтенда и бэкенда.
Что такое XSS и как его предотвратить?
XSS (Cross-Site Scripting) – это атака, при которой злоумышленник внедряет вредоносный JavaScript-код в веб-страницу.Она может использоваться для кражи данных, изменения интерфейса и других вредоносных действий.
Способы защиты от XSS:
- Экранирование пользовательского ввода (`escape()` и `encodeURIComponent()`).
- Использование `Content Security Policy (CSP)`.
- Очистка HTML-контента с помощью библиотек (например, `DOMPurify`).

// Очистка HTML перед вставкой в DOM (использование DOMPurify)
const cleanHTML = DOMPurify.sanitize(userInput);
document.getElementById("output").innerHTML = cleanHTML;

Что такое CSRF и как его предотвратить?
CSRF (Cross-Site Request Forgery) – это атака, при которой злоумышленник выполняет действия от имени пользователя без его ведома.
Способы защиты от CSRF:
- Использование **CSRF-токенов** (запросы должны содержать уникальный токен).
- Проверка `Referer` и `Origin` заголовков.
- Ограничение `SameSite` для cookies.

// Настройка SameSite для cookies (на бэкенде)
Set-Cookie: session=abc123; HttpOnly; Secure; SameSite=Strict

Что такое Content Security Policy (CSP)?
CSP – это механизм, который ограничивает выполнение вредоносного JavaScript-кода, защищая от XSS-атак.

// Установка заголовка CSP на сервере
Content-Security-Policy: default-src 'self'; script-src 'self' 'https://trusted.com';

Как защититься от SQL-инъекций в JavaScript?
SQL-инъекции происходят, когда злоумышленник внедряет SQL-код в запросы к базе данных.
Способы защиты:
- Использование **подготовленных SQL-запросов (Prepared Statements)**.
- Валидация и экранирование пользовательского ввода.
- Использование ORM (Sequelize, Prisma).

// Использование подготовленного запроса в Node.js (PostgreSQL)
const query = "SELECT * FROM users WHERE username = $1";
const result = await db.query(query, [userInput]);

Как безопасно работать с JWT?
JWT (JSON Web Token) используется для аутентификации, но при неправильной настройке может быть уязвим.
Способы защиты:
- Подписывайте токены с помощью **секретного ключа** или RSA.
- Используйте **короткий срок жизни токена** (`exp`).
- Храните JWT в **HttpOnly cookies**, а не в `localStorage`.

// Генерация JWT с истечением через 1 час (Node.js)
const jwt = require('jsonwebtoken');
const token = jwt.sign({ userId: 123 }, "SECRET_KEY", { expiresIn: '1h' });

Безопасность в JavaScript включает защиту от XSS, CSRF, SQL-инъекций, а также правильное использование CSP и JWT.
 
Тестирование в JavaScript
Тестирование – важная часть разработки, позволяющая выявлять ошибки и обеспечивать стабильность кода. Существуют разные виды тестирования: модульное, интеграционное и end-to-end (E2E).
Какие виды тестирования бывают в JavaScript?
Основные виды тестирования:
- **Unit-тестирование** – проверка отдельных функций и компонентов.
- **Integration-тестирование** – тестирование взаимодействия между модулями.
- **E2E-тестирование** – тестирование всего приложения с точки зрения пользователя.
Что такое Unit, Integration, E2E тесты?
- **Unit-тесты** – тестируют отдельные функции/модули.
- **Integration-тесты** – проверяют, как взаимодействуют разные части приложения.
- **E2E-тесты** – имитируют действия пользователя в приложении.
Как работает Jest и Mocha?
Jest и Mocha – популярные инструменты для тестирования JavaScript.
- **Jest** – удобен для тестирования React и Node.js.
- **Mocha** – гибкий тест-раннер для браузера и Node.js.

// Unit-тест на Jest
const sum = (a, b) => a + b;

test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
});


// Тестирование на Mocha + Chai
const { expect } = require("chai");

describe("Сложение чисел", function() {
    it("1 + 2 должно быть равно 3", function() {
        expect(1 + 2).to.equal(3);
    });
});

Что такое Snapshot Testing?
Snapshot-тестирование позволяет проверять, не изменился ли вывод компонента с момента последнего теста.

// Тест Snapshot в Jest (React)
import renderer from 'react-test-renderer';
import MyComponent from './MyComponent';

test('рендер компонента', () => {
    const tree = renderer.create(<MyComponent />).toJSON();
    expect(tree).toMatchSnapshot();
});

Тестирование JavaScript-кода позволяет избежать ошибок, улучшить качество кода и обеспечить стабильную работу приложения.
TypeScript
1. Основы TypeScript
TypeScript — это надстройка над JavaScript, которая добавляет статическую типизацию и помогает избежать ошибок в коде.
Что такое TypeScript и чем он отличается от JavaScript?
TypeScript — это язык программирования, расширяющий JavaScript за счет статической типизации. TypeScript компилируется в JavaScript и может работать в любом браузере.
Основные отличия TypeScript от JavaScript:
- **Статическая типизация**: позволяет находить ошибки на этапе компиляции.
- **Интерфейсы и дженерики**: улучшают архитектуру кода.
- **Совместимость с JavaScript**: весь код на JS — это валидный TypeScript.
- **Продвинутые возможности ООП**: классы, абстрактные классы, модификаторы доступа.
Какие преимущества дает TypeScript?
Основные преимущества TypeScript:
- **Уменьшение количества ошибок** за счет строгой типизации.
- **Улучшенная поддержка IDE**: автодополнение, рефакторинг, поиск типов.
- **Совместимость с JavaScript**: можно постепенно внедрять TS в проект.
- **Лучшая документация кода**: типы данных служат как документация.
Как установить TypeScript и скомпилировать код?
Установка TypeScript глобально:

npm install -g typescript

Создание файла `app.ts` и его компиляция в JavaScript:

tsc app.ts

Что такое `tsconfig.json` и зачем он нужен?
Файл `tsconfig.json` содержит настройки компилятора TypeScript и управляет поведением компиляции.
Пример `tsconfig.json`:

{
  "compilerOptions": {
    "target": "ES6",
    "module": "CommonJS",
    "strict": true,
    "outDir": "./dist",
    "rootDir": "./src"
  }
}

Чем `let`, `const` и `var` отличаются в TypeScript?
Различия между `let`, `const` и `var`:
- `let` – блочная область видимости, можно изменять значение.
- `const` – блочная область видимости, нельзя изменять значение.
- `var` – функциональная область видимости, избегать использования.
Пример использования:

let a = 10;   // Можно изменить
const b = 20; // Нельзя изменить
var c = 30;   // Устаревший способ объявления переменных

TypeScript делает разработку безопаснее и удобнее за счет строгой типизации и улучшенной поддержки IDE. Следующим шагом можно рассмотреть типизацию в TypeScript.
 
2. Типизация в TypeScript
TypeScript добавляет строгую типизацию к JavaScript, что помогает избежать многих ошибок и делает код более предсказуемым.
Какие основные типы данных есть в TypeScript?
TypeScript поддерживает следующие основные типы данных:
- **string** – строковые значения.
- **number** – целые и дробные числа.
- **boolean** – логические значения (true/false).
- **array** – массивы (`number[]`, `string[]`).
- **tuple** – кортежи фиксированной длины (`[string, number]`).
- **enum** – перечисления.
- **any** – отключает проверку типов.
- **unknown** – безопасная альтернатива `any`.
- **void** – функция, которая ничего не возвращает.
- **null и undefined** – отсутствие значения.
- **never** – функции, которые никогда не завершаются.
Как объявить переменные с явным типом?
Пример объявления переменных с типами:

let userName: string = "Alice";
let age: number = 30;
let isAdmin: boolean = true;
let numbers: number[] = [1, 2, 3, 4];
let user: [string, number] = ["Alice", 30]; // Tuple

Что такое `any`, `unknown`, `void`, `never` и в чем их разница?
Различия между этими типами:
- **any** – отключает проверку типов (использовать с осторожностью).
- **unknown** – аналог `any`, но требует явного приведения типов.
- **void** – функция, которая ничего не возвращает.
- **never** – функция, которая никогда не завершится (например, `throw`).
Пример использования:

function logMessage(message: string): void {
    console.log(message);
}

function throwError(): never {
    throw new Error("Something went wrong!");
}

Чем `type` отличается от `interface`?
Оба позволяют задавать структуры данных, но есть различия:
- **interface** используется для описания объектов и классов.
- **type** может объединять примитивные типы, использовать `union` и `intersection`.
Пример `interface`:

interface User {
    name: string;
    age: number;
}

const user: User = { name: "Alice", age: 30 };

Пример `type`:

type ID = string | number;

let userId: ID = 123;
userId = "abc"; // Работает, так как ID — это string или number

Как использовать `readonly` и `const`?
`readonly` делает свойства неизменяемыми в объектах, `const` – для переменных.

interface Car {
    readonly brand: string;
}

const myCar: Car = { brand: "Toyota" };
myCar.brand = "Honda"; // Ошибка, так как свойство readonly

const MAX_USERS = 100; // Константа

Как работает `type inference` в TypeScript?
TypeScript сам определяет тип переменной, если явно его не указать.

let message = "Hello, TypeScript!"; // TypeScript автоматически определяет тип как string

let count = 10; // TypeScript определит number

Что такое `union` и `intersection` типы?
**Union** позволяет использовать несколько типов, **Intersection** объединяет типы.

// Union (переменная может быть number или string)
let id: number | string = 123;
id = "ABC"; // Работает

// Intersection (объединение типов)
type Person = { name: string };
type Employee = { company: string };

type Worker = Person & Employee; // Объединение типов

const worker: Worker = { name: "Alice", company: "Google" };

Как объявить `tuple` и `enum`?
Tuple – это массив фиксированной длины, Enum – набор предопределенных значений.

// Tuple
let person: [string, number] = ["Alice", 30];

// Enum
enum Role { Admin, User, Guest }
let myRole: Role = Role.Admin;

Типизация в TypeScript помогает писать безопасный код, предотвращая ошибки на этапе компиляции. Следующим шагом можно рассмотреть работу с функциями.
 
3. Функции в TypeScript
Функции в TypeScript позволяют объявлять аргументы с типами, определять возвращаемые значения и использовать перегрузку.
Как объявить функции в TypeScript?
Пример объявления функции с параметрами и возвращаемым типом:

function add(a: number, b: number): number {
    return a + b;
}

console.log(add(5, 10)); // 15

Что такое перегрузка функций (`function overloading`)?
Перегрузка функций позволяет объявлять несколько сигнатур с разными типами аргументов.
Пример перегрузки:

function greet(name: string): string;
function greet(name: string, age: number): string;

function greet(name: string, age?: number): string {
    return age ? `Hello, ${name}. You are ${age} years old.` : `Hello, ${name}.`;
}

console.log(greet("Alice")); // Hello, Alice.
console.log(greet("Bob", 30)); // Hello, Bob. You are 30 years old.

Как определить тип аргументов и возвращаемого значения?
Можно явно указывать типы аргументов и возвращаемого значения.

function multiply(a: number, b: number): number {
    return a * b;
}

console.log(multiply(4, 5)); // 20

Как работают опциональные параметры и значения по умолчанию?
Опциональные параметры обозначаются `?`, а значения по умолчанию задаются `=`.

function greetUser(name: string, age?: number): string {
    return age ? `Hello, ${name}. You are ${age}.` : `Hello, ${name}.`;
}

function power(base: number, exponent: number = 2): number {
    return Math.pow(base, exponent);
}

console.log(greetUser("Alice")); // Hello, Alice.
console.log(power(3)); // 9 (3^2)
console.log(power(3, 3)); // 27 (3^3)

Чем `never` отличается от `void`?
`void` используется для функций, которые ничего не возвращают, а `never` – для функций, которые никогда не завершаются.

function logMessage(message: string): void {
    console.log(message);
}

function throwError(): never {
    throw new Error("Critical Error!");
}

Функции в TypeScript позволяют явно указывать типы параметров и возвращаемых значений, что делает код более безопасным. Следующим шагом можно рассмотреть объекты и интерфейсы.
 
4. Объекты и интерфейсы в TypeScript
TypeScript позволяет описывать объекты с помощью интерфейсов и типов. Это делает код более читаемым и предотвращает ошибки при работе с объектами.
Как создать объект с определенной структурой?
Можно задать структуру объекта с помощью интерфейсов или типов.

type User = {
    name: string;
    age: number;
    isAdmin: boolean;
};

const user: User = {
    name: "Alice",
    age: 25,
    isAdmin: false
};

Чем `interface` отличается от `type`?
Основные различия между `interface` и `type`:
- `interface` чаще используется для описания объектов и классов.
- `type` может описывать объекты, объединять примитивные типы (`union`) и накладывать ограничения.
Пример интерфейса:

interface User {
    name: string;
    age: number;
}

const user: User = { name: "Alice", age: 30 };

Пример `type`:

type ID = string | number;

let userId: ID = 123;
userId = "abc"; // Допустимо

Как расширять интерфейсы (`extends`)?
Можно расширять интерфейсы с помощью `extends`.

interface Person {
    name: string;
    age: number;
}

interface Employee extends Person {
    position: string;
}

const employee: Employee = {
    name: "Bob",
    age: 28,
    position: "Developer"
};

Как создать объект с динамическими ключами?
Если ключи объекта неизвестны заранее, можно использовать `index signature`.

interface UserDictionary {
    [key: string]: string;
}

const users: UserDictionary = {
    alice: "Alice Johnson",
    bob: "Bob Smith"
};

Как сделать частично или полностью неизменяемый объект?
Можно использовать `readonly` или `Partial<>` и `Readonly<>`.

interface User {
    readonly id: number;
    name: string;
}

const user: User = { id: 1, name: "Alice" };
user.id = 2; // Ошибка, так как id readonly

// Частично изменяемый объект
const updatedUser: Partial<User> = { name: "Bob" };

// Полностью неизменяемый объект
const frozenUser: Readonly<User> = { id: 1, name: "Alice" };
frozenUser.name = "Bob"; // Ошибка

Объекты и интерфейсы в TypeScript позволяют описывать структуру данных, делая код безопаснее и понятнее. Следующим шагом можно рассмотреть классы и ООП в TypeScript.
 
5. Классы и ООП в TypeScript
TypeScript предоставляет мощные инструменты для объектно-ориентированного программирования. Классы в TypeScript позволяют создавать объекты, наследоваться, использовать интерфейсы и контролировать доступ к данным.
Как объявить класс в TypeScript?
Пример простого класса:

class User {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    greet(): string {
        return `Hello, my name is ${this.name}.`;
    }
}

const user = new User("Alice", 30);
console.log(user.greet());

Чем `public`, `private`, `protected` отличаются?
Модификаторы доступа определяют, как можно обращаться к свойствам и методам класса:
- **public** – свойства и методы доступны везде.
- **private** – доступны только внутри класса.
- **protected** – доступны внутри класса и его потомков.

class Employee {
    public name: string;
    private salary: number;
    protected department: string;

    constructor(name: string, salary: number, department: string) {
        this.name = name;
        this.salary = salary;
        this.department = department;
    }

    public showName(): string {
        return this.name;
    }
}

Как использовать `abstract` классы?
Абстрактные классы позволяют задавать общую структуру для дочерних классов.

abstract class Shape {
    abstract getArea(): number;

    describe(): string {
        return "This is a shape.";
    }
}

class Rectangle extends Shape {
    width: number;
    height: number;

    constructor(width: number, height: number) {
        super();
        this.width = width;
        this.height = height;
    }

    getArea(): number {
        return this.width * this.height;
    }
}

Что такое геттеры и сеттеры (`get`, `set`)?
Геттеры и сеттеры позволяют контролировать доступ к свойствам класса.

class Person {
    private _age: number;

    constructor(age: number) {
        this._age = age;
    }

    get age(): number {
        return this._age;
    }

    set age(value: number) {
        if (value >= 0) {
            this._age = value;
        } else {
            throw new Error("Age must be non-negative");
        }
    }
}

Как работает `implements` и `extends`?
`implements` используется для реализации интерфейса, `extends` – для наследования класса.

interface Driveable {
    drive(): void;
}

class Car implements Driveable {
    drive() {
        console.log("Driving a car...");
    }
}

class ElectricCar extends Car {
    charge() {
        console.log("Charging the car...");
    }
}

Что такое `static` свойства и методы?
`static` свойства и методы принадлежат самому классу, а не его экземплярам.

class Calculator {
    static add(a: number, b: number): number {
        return a + b;
    }
}

console.log(Calculator.add(5, 10)); // 15

Классы в TypeScript обеспечивают мощные возможности для создания сложных приложений. Следующим шагом можно рассмотреть дженерики в TypeScript.
 
6. Дженерики (Generics)
Дженерики в TypeScript позволяют создавать обобщенные функции, интерфейсы и классы, которые могут работать с разными типами данных.
Что такое дженерики и зачем они нужны?
Дженерики – это способ сделать код более универсальным, позволяющий использовать разные типы данных без явного указания типа в каждом случае.

// Пример без дженериков
function identity(arg: number): number {
    return arg;
}

// Пример с дженериками
function identity<T>(arg: T): T {
    return arg;
}

const output1 = identity<string>("Hello");
const output2 = identity<number>(42);

Как объявить обобщенные функции (`generic functions`)?
Обобщенные функции объявляются с использованием параметров типа:

function reverseArray<T>(items: T[]): T[] {
    return items.reverse();
}

const numbers = [1, 2, 3, 4];
const reversedNumbers = reverseArray<number>(numbers);

const strings = ["a", "b", "c"];
const reversedStrings = reverseArray<string>(strings);

Как использовать дженерики с интерфейсами и классами?
Дженерики можно использовать в интерфейсах и классах для работы с разными типами.

interface Repository<T> {
    getById(id: number): T;
    getAll(): T[];
}

class UserRepository implements Repository<User> {
    getById(id: number): User {
        // логика получения пользователя
    }
    getAll(): User[] {
        // логика получения всех пользователей
    }
}

Что такое `T extends`?
`T extends` задает ограничения для дженериков, чтобы они соответствовали определенному типу.

function printName<T extends { name: string }>(item: T): void {
    console.log(item.name);
}

const user = { name: "Alice", age: 30 };
printName(user); // Работает, так как user имеет свойство name

Как задать ограничения (`constraints`) для дженериков?
Ограничения позволяют гарантировать, что дженерик будет соответствовать определенной структуре или типу.

// Пример ограничения с extends
function getLength<T extends { length: number }>(item: T): number {
    return item.length;
}

const array = [1, 2, 3];
console.log(getLength(array)); // 3

Дженерики – это мощный инструмент TypeScript, который позволяет писать гибкий и переиспользуемый код. Следующим шагом можно рассмотреть работу с модулями в TypeScript.
 
7. Работа с модулями
Модули в TypeScript помогают разделять код на логически связанные части и управлять зависимостями.
Как работают модули в TypeScript?
TypeScript использует `import` и `export` для работы с модулями. Код, который экспортируется из одного файла, можно импортировать в другой.

// mathUtils.ts
export function add(a: number, b: number): number {
    return a + b;
}

// main.ts
import { add } from "./mathUtils";

console.log(add(5, 10)); // 15

В чем разница между `import/export` и `require/module.exports`?
- `import/export` – это современный стандарт ES6.
- `require/module.exports` – это CommonJS, используемый в Node.js.
Пример `import/export` (ES6):

// utils.ts
export const greet = (name: string) => `Hello, ${name}!`;

// main.ts
import { greet } from "./utils";
console.log(greet("Alice"));

Пример `require/module.exports` (CommonJS):

// utils.js
module.exports.greet = (name) => `Hello, ${name}!`;

// main.js
const utils = require("./utils");
console.log(utils.greet("Alice"));

Что такое `namespace` и когда его использовать?
Namespace – это способ организовать код в одной области видимости. Он полезен для группировки связанных функций и типов в одном модуле.

namespace Utils {
    export function add(a: number, b: number): number {
        return a + b;
    }

    export function multiply(a: number, b: number): number {
        return a * b;
    }
}

// Использование
const sum = Utils.add(5, 10);
const product = Utils.multiply(3, 4);

Работа с модулями делает код более структурированным и удобным для сопровождения. Следующим шагом можно рассмотреть TypeScript в сочетании с JavaScript.
 
8. TypeScript и JavaScript
TypeScript является надстройкой над JavaScript, поэтому весь существующий код на JS можно использовать в TypeScript. Это делает переход на TypeScript плавным.
Как использовать TypeScript с существующим JavaScript кодом?
TypeScript может компилировать файлы с расширением `.js` так же, как `.ts`. Это позволяет постепенно интегрировать TypeScript в проект.

// tsconfig.json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true
  }
}

С этими настройками можно использовать существующий JavaScript код и постепенно добавлять аннотации типов.
Чем отличается `declare` от `type`?
Ключевое слово `declare` используется для объявления переменных, функций и модулей, которые уже существуют в JavaScript, но не имеют аннотаций типов.

declare const ENV: string;
console.log(ENV);

`type` используется для создания новых типов:

type UserID = string | number;
let id: UserID = 123;

Что такое Ambient Declaration (`.d.ts` файлы)?
Файлы `.d.ts` содержат декларации типов для существующих JavaScript библиотек. Они используются для получения автодополнения и проверки типов в TypeScript.
Пример `d.ts` файла:

// utils.d.ts
declare function greet(name: string): string;

Теперь в TypeScript можно использовать `greet` с проверкой типов:

greet("Alice");

TypeScript позволяет использовать существующий JavaScript код, добавляя типы и улучшая качество кода. Следующим шагом можно рассмотреть работу с конфигурацией TypeScript.
 
9. Работа с конфигурацией TypeScript
Конфигурация TypeScript управляется с помощью файла `tsconfig.json`. Этот файл позволяет настроить компилятор, определить строгие проверки типов и указать целевую версию JavaScript.
Какие самые важные настройки в `tsconfig.json`?
Некоторые из ключевых настроек:
- **`target`**: указывает версию JavaScript, в которую компилируется TypeScript (например, `ES6`, `ES5`).
- **`module`**: определяет систему модулей (например, `CommonJS`, `ESNext`).
- **`strict`**: включает строгий режим компиляции.
- **`outDir` и `rootDir`**: указывают, где искать исходные файлы и куда сохранять скомпилированные.

{
  "compilerOptions": {
    "target": "ES6",
    "module": "CommonJS",
    "strict": true,
    "outDir": "./dist",
    "rootDir": "./src"
  }
}

Что такое `strict mode`?
Включение `strict` активирует несколько строгих проверок, таких как `noImplicitAny` и `strictNullChecks`. Это помогает находить потенциальные ошибки на этапе компиляции.

{
  "compilerOptions": {
    "strict": true
  }
}

С включенным `strict` TypeScript будет требовать явного указания типов и проверки на null/undefined.
Как настроить путь к модулям (`paths`)?
С помощью `paths` можно задать алиасы для директорий, чтобы упростить импорт модулей.

{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@app/*": ["src/app/*"],
      "@utils/*": ["src/utils/*"]
    }
  }
}

Теперь вместо длинных относительных путей можно использовать алиасы: `import { func } from "@utils/helpers";`.
Как компилировать TypeScript в JavaScript (`target`)?
Опция `target` определяет, в какой стандарт JavaScript будет компилироваться TypeScript.

{
  "compilerOptions": {
    "target": "ES6"
  }
}

При указании `target: "ES6"` скомпилированный код будет использовать современные возможности JavaScript, такие как `let` и `const`. Указание `target: "ES5"` обеспечит совместимость с более старыми окружениями.
Настройка `tsconfig.json` – это важный этап работы с TypeScript, позволяющий управлять компиляцией и строгими проверками. Следующим шагом можно рассмотреть использование TypeScript с React.
 
10. TypeScript и React
TypeScript предоставляет мощные инструменты для типизации React-компонентов, хуков и пропсов, что делает разработку компонентов более безопасной и удобной.
Как использовать TypeScript в React?
Для начала необходимо установить типы для React и ReactDOM:

npm install --save-dev @types/react @types/react-dom

Затем создайте файлы с расширением `.tsx` вместо `.jsx` и добавьте типы для пропсов и состояний.
Как типизировать `useState`, `useRef`, `useEffect`?
Примеры типизации хуков в React:

import { useState, useEffect, useRef } from "react";

// useState с начальным значением и типом
const [count, setCount] = useState<number>(0);

// useRef для DOM элемента
const inputRef = useRef<HTMLInputElement>(null);

// useEffect с типами для очистки
useEffect(() => {
  const handleResize = () => {
    console.log("Window resized");
  };

  window.addEventListener("resize", handleResize);
  return () => window.removeEventListener("resize", handleResize);
}, []);

Как передавать `props` в компоненты?
Props можно типизировать с помощью интерфейсов или типов. Пример функционального компонента с типизированными пропсами:

interface ButtonProps {
  text: string;
  onClick: () => void;
}

const Button: React.FC<ButtonProps> = ({ text, onClick }) => (
  <button onClick={onClick}>{text}</button>
);

Как типизировать `children`?
Для типизации `children` можно использовать `React.ReactNode`:

interface ContainerProps {
  children: React.ReactNode;
}

const Container: React.FC<ContainerProps> = ({ children }) => (
  <div className="container">{children}</div>
);

Как использовать `React.FC` и почему он устарел?
Ранее `React.FC` использовался для типизации компонентов, включая `children`. Однако сейчас рекомендуется использовать простые функции и явно указывать типы пропсов. Это позволяет избежать проблем с `defaultProps` и улучшает читаемость.

// Предпочтительный подход
type ButtonProps = {
  text: string;
  onClick: () => void;
};

const Button = ({ text, onClick }: ButtonProps) => (
  <button onClick={onClick}>{text}</button>
);

TypeScript и React – мощное сочетание для создания надежных интерфейсов с четкой типизацией. Следующим шагом можно рассмотреть использование TypeScript в бекенд-разработке.
 
11. TypeScript в Backend (NestJS, Express)
TypeScript идеально подходит для бекенд-разработки, особенно в сочетании с фреймворками NestJS и Express. Он обеспечивает строгую типизацию маршрутов, middleware, DTO и валидаторов.
Как использовать TypeScript в Node.js?
Для использования TypeScript в Node.js:
1. Установите TypeScript и необходимые типы:
```bash
npm install typescript @types/node --save-dev
```
2. Создайте `tsconfig.json` и настройте его под Node.js:
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "CommonJS",
    "strict": true,
    "outDir": "./dist",
    "rootDir": "./src"
  }
}
```
3. Напишите серверный код в файлах с расширением `.ts` и скомпилируйте их командой `tsc`.
Как типизировать API в Express?
В Express можно использовать типы для объектов запроса, ответа и middleware. Пример типизации маршрута:

import { Request, Response } from 'express';

app.get('/user', (req: Request, res: Response) => {
  res.json({ name: 'Alice', age: 30 });
});

Типизация упрощает автодополнение в IDE и позволяет находить ошибки до выполнения кода.
Как работать с DTO в NestJS?
DTO (Data Transfer Object) – это объект, который описывает структуру данных, передаваемых между клиентом и сервером. В NestJS DTO обычно оформляются как классы с аннотациями для валидации.

import { IsString, IsInt } from 'class-validator';

export class CreateUserDto {
  @IsString()
  name: string;

  @IsInt()
  age: number;
}

Использование DTO делает код более предсказуемым и предотвращает передачу некорректных данных.
Как использовать `class-validator` и `class-transformer`?
`class-validator` позволяет проверять данные на основе аннотаций, а `class-transformer` – преобразовывать данные. Например, вы можете преобразовать строковые параметры запроса в числа и сразу валидировать их.

import { Type } from 'class-transformer';
import { IsInt, Min } from 'class-validator';

export class GetUserDto {
  @Type(() => Number)
  @IsInt()
  @Min(1)
  id: number;
}

При получении данных из маршрута они автоматически преобразуются в указанные типы и проверяются на соответствие требованиям.
TypeScript в бекенде делает разработку API удобнее и безопаснее, позволяя использовать строгую типизацию и встроенные инструменты для валидации данных. Следующим шагом можно рассмотреть продвинутые темы в TypeScript.
 
12. Продвинутые темы
TypeScript предоставляет множество продвинутых возможностей для работы с типами, таких как условные типы, встроенные вспомогательные типы, и оператор `keyof`.
Что такое Mapped Types (`Partial<T>`, `Readonly<T>` и т.д.)?
Mapped Types позволяют создавать новые типы на основе существующих. Например, можно сделать все поля объекта необязательными или только для чтения.

interface User {
  name: string;
  age: number;
}

type PartialUser = Partial<User>; // Все поля становятся необязательными
type ReadonlyUser = Readonly<User>; // Все поля становятся только для чтения

Как работает `keyof`?
`keyof` используется для получения набора ключей типа. Это удобно, если нужно явно указать, что переменная будет принимать одно из полей объекта.

interface User {
  name: string;
  age: number;
}

type UserKeys = keyof User; // "name" | "age"

function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Alice", age: 30 };
const userName = getValue(user, "name"); // OK

Что такое `infer`?
Ключевое слово `infer` позволяет извлечь тип внутри условного типа. Это полезно, если нужно вывести тип, переданный в функцию или другую конструкцию.

type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

function add(a: number, b: number): number {
  return a + b;
}

type AddReturnType = ReturnType<typeof add>; // number

Как использовать `conditional types`?
Условные типы позволяют создавать типы на основе условий. Синтаксис: `T extends U ? X : Y`.

type IsString<T> = T extends string ? true : false;

type Test1 = IsString<string>; // true
type Test2 = IsString<number>; // false

Как работает `typeof` в TypeScript?
`typeof` используется для получения типа переменной или функции. Это полезно, если нужно создать тип на основе существующего значения.

const user = {
  name: "Alice",
  age: 30
};

type UserType = typeof user; // { name: string; age: number; }

Продвинутые возможности TypeScript позволяют создавать гибкие типы и выстраивать сложные модели данных. Это делает TypeScript мощным инструментом для крупных и сложных проектов.





 
Node.js
Основы Node.js
Node.js – это среда выполнения JavaScript на сервере, основанная на движке V8. Она позволяет писать серверный код на JavaScript, работая с файлами, базами данных, сетевыми запросами и многим другим.
Что такое Node.js и чем он отличается от браузерного JavaScript?
Node.js позволяет выполнять JavaScript-код на сервере, а не в браузере. Основные отличия:
- В Node.js нет `window`, `document` и других браузерных API.
- Node.js имеет встроенные модули (`fs`, `http`, `path` и др.).
- Использует Event Loop для асинхронных операций без блокировки.

// Пример кода на Node.js
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, Node.js!');
});

server.listen(3000, () => console.log('Сервер запущен на порту 3000'));

Как работает V8 и в чем его преимущества?
V8 – это JavaScript-движок от Google, используемый в Chrome и Node.js. Он компилирует JavaScript в машинный код, что делает его быстрым.
Преимущества:
- Высокая производительность благодаря JIT-компиляции.
- Оптимизации (Inline Caching, Hidden Classes и др.).
- Поддержка современных версий ECMAScript.
Что такое Event Loop и как он работает в Node.js?
Event Loop – это механизм, который позволяет Node.js выполнять асинхронные операции без блокировки основного потока.

// Демонстрация Event Loop
console.log('Начало');

setTimeout(() => {
    console.log('Таймер 1 секунда');
}, 1000);

setImmediate(() => console.log('Immediate'));

process.nextTick(() => console.log('Next Tick'));

console.log('Конец');

В этом примере сначала выполняются синхронные операции (`Начало`, `Конец`). Затем `nextTick` срабатывает раньше, чем `setImmediate`, а `setTimeout` выполняется через 1 секунду.
В чем разница между CommonJS (require) и ESModules (import/export)?
- **CommonJS (`require`)** – используется в Node.js по умолчанию, синхронный.
- **ESModules (`import/export`)** – поддерживается в современных версиях, асинхронный.

// CommonJS (require)
const fs = require('fs');

// ESModules (import/export)
import fs from 'fs';

Чем отличается synchronous и asynchronous код в Node.js?
- **Синхронный код** выполняется последовательно, блокируя поток.
- **Асинхронный код** использует коллбэки, промисы (`Promise`), `async/await`, позволяя выполнять другие задачи в ожидании результата.

// Синхронное чтение файла (блокирующее)
const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);

// Асинхронное чтение файла (не блокирующее)
fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

Node.js – мощная платформа для серверного JavaScript, использующая V8 и Event Loop для высокопроизводительных асинхронных приложений.
 
Работа с модулями и пакетами в Node.js
Node.js использует модульную систему, позволяя разделять код на отдельные файлы. Модули могут быть встроенными, локальными или загруженными из npm.
Как создать и подключить модуль в Node.js?
В Node.js можно создавать собственные модули и подключать их с помощью `require()` (CommonJS) или `import` (ESModules).

// myModule.js (модуль)
module.exports = function greet(name) {
    return `Привет, ${name}!`;
};

// index.js (подключение модуля)
const greet = require('./myModule');
console.log(greet('Алиса')); // Привет, Алиса!

Что такое npm и как им пользоваться?
npm (Node Package Manager) – это менеджер пакетов для Node.js. Он используется для установки, обновления и управления зависимостями.

// Инициализация нового проекта
npm init -y

// Установка пакета (например, Express)
npm install express

// Удаление пакета
npm uninstall express

Чем отличается dependencies от devDependencies?
- **dependencies** – пакеты, которые необходимы в продакшене.
- **devDependencies** – пакеты, нужные только во время разработки (например, тестирование).

// Установка пакета в dependencies
npm install express --save

// Установка пакета в devDependencies
npm install jest --save-dev

Как использовать package.json и package-lock.json?
`package.json` – это файл, который содержит информацию о проекте и его зависимостях.
`package-lock.json` – это файл, фиксирующий точные версии установленных пакетов.

// Часть package.json
{
  "name": "my-project",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "jest": "^27.0.0"
  }
}

Что такое npx и как он используется?
npx (Node Package Execute) позволяет запускать пакеты без предварительной установки в проект.

// Запуск пакета без установки
npx create-react-app my-app

// Проверка версии Node.js
npx node -v

Модули и пакеты в Node.js помогают организовывать код, а npm упрощает установку и управление зависимостями.
 
Работа с файловой системой (fs) в Node.js
Модуль `fs` в Node.js позволяет работать с файлами и директориями – читать, записывать, удалять и изменять их.
Как читать и записывать файлы в Node.js?
В Node.js файлы можно читать и записывать как синхронно, так и асинхронно.

// Подключение модуля fs
const fs = require('fs');

// Чтение файла (асинхронно)
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

// Запись в файл (асинхронно)
fs.writeFile('example.txt', 'Hello, Node.js!', (err) => {
    if (err) throw err;
    console.log('Файл записан');
});

В чем разница между fs.readFile() и fs.createReadStream()?
- `fs.readFile()` загружает весь файл в память, что может быть неэффективно для больших файлов.
- `fs.createReadStream()` читает файл потоками, что снижает нагрузку на память.

// Чтение файла целиком (неэффективно для больших файлов)
fs.readFile('large.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

// Чтение файла потоками (оптимально для больших файлов)
const stream = fs.createReadStream('large.txt', 'utf8');
stream.on('data', chunk => console.log('Читаем кусок:', chunk));

Как использовать fs.promises для работы с файлами?
Модуль `fs.promises` позволяет работать с файлами с использованием `async/await`, что делает код чище и понятнее.

// Работа с файлами с использованием fs.promises
const fs = require('fs').promises;

async function readAndWriteFile() {
    try {
        const data = await fs.readFile('example.txt', 'utf8');
        console.log('Содержимое файла:', data);

        await fs.writeFile('newFile.txt', 'Новый контент');
        console.log('Файл успешно записан');
    } catch (error) {
        console.error('Ошибка:', error);
    }
}

readAndWriteFile();

Как обработать ошибки при работе с файлами?
При работе с файлами могут возникать ошибки (например, файл не найден). Их нужно обрабатывать через `try/catch` или `callback` функции.

fs.readFile('nonexistent.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Ошибка при чтении файла:', err.message);
        return;
    }
    console.log(data);
});

// Обработка ошибок с async/await
async function safeReadFile() {
    try {
        const data = await fs.promises.readFile('nonexistent.txt', 'utf8');
        console.log(data);
    } catch (error) {
        console.error('Ошибка при чтении файла:', error.message);
    }
}

safeReadFile();

Модуль `fs` в Node.js позволяет эффективно работать с файлами, используя как синхронные, так и асинхронные методы, а также потоки для обработки больших файлов.
 
Потоки (Streams) и буферы (Buffers) в Node.js
Потоки (Streams) в Node.js позволяют работать с данными постепенно, а не загружать их в память целиком. Буферы (Buffers) используются для хранения бинарных данных, например, при работе с файлами и сетью.
Что такое Streams и какие они бывают?
Streams – это последовательные потоки данных, которые можно читать или записывать по частям. Они используются для обработки больших файлов и работы с сетью.
Виды потоков в Node.js:
- **Readable** – потоки для чтения данных.
- **Writable** – потоки для записи данных.
- **Duplex** – двусторонние потоки (чтение и запись).
- **Transform** – потоки, которые могут изменять данные в процессе передачи.

// Чтение файла через поток
const fs = require('fs');

const readStream = fs.createReadStream('bigfile.txt', 'utf8');
readStream.on('data', chunk => {
    console.log('Получен кусок данных:', chunk);
});

readStream.on('end', () => console.log('Чтение завершено'));

Как работают Readable, Writable, Duplex и Transform Streams?
Примеры различных потоков:

// Writable Stream (запись в файл)
const writeStream = fs.createWriteStream('output.txt');
writeStream.write('Привет, потоковая запись!\n');
writeStream.end();

// Duplex Stream (чтение и запись)
const { Duplex } = require('stream');
const duplexStream = new Duplex({
    read(size) {
        this.push('Данные');
        this.push(null);
    },
    write(chunk, encoding, callback) {
        console.log('Полученные данные:', chunk.toString());
        callback();
    }
});

duplexStream.write('Тест данных');
duplexStream.pipe(process.stdout);

// Transform Stream (изменение данных)
const { Transform } = require('stream');
const transformStream = new Transform({
    transform(chunk, encoding, callback) {
        this.push(chunk.toString().toUpperCase());
        callback();
    }
});

process.stdin.pipe(transformStream).pipe(process.stdout);

Что такое pipe() и как его использовать?
Метод `pipe()` позволяет передавать данные из одного потока в другой, например, читать данные из файла и сразу записывать их в другой файл.

// Копирование файла с использованием pipe()
const readStream = fs.createReadStream('input.txt');
const writeStream = fs.createWriteStream('output.txt');

readStream.pipe(writeStream);

readStream.on('end', () => console.log('Копирование завершено'));

Как работают Buffer и зачем он нужен?
Buffer – это объект для работы с бинарными данными в памяти. Он используется при чтении файлов, обработке изображений и сетевом обмене.

// Создание буфера из строки
const buffer = Buffer.from('Hello, Node.js');
console.log(buffer.toString()); // Hello, Node.js

// Создание пустого буфера и запись в него
const newBuffer = Buffer.alloc(10);
newBuffer.write('Test');
console.log(newBuffer.toString()); // Test

Потоки позволяют эффективно работать с данными без загрузки всего файла в память, а буферы обеспечивают работу с бинарными данными.
 
HTTP-сервер в Node.js
Node.js позволяет создавать HTTP-серверы без использования сторонних библиотек. Для этого используется встроенный модуль `http`.
Как создать простой HTTP-сервер без Express?
Node.js предоставляет модуль `http`, который позволяет обрабатывать запросы и отправлять ответы.

// Подключаем модуль http
const http = require('http');

// Создаём сервер
const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, Node.js!');
});

// Запуск сервера на порту 3000
server.listen(3000, () => {
    console.log('Сервер запущен на http://localhost:3000');
});

Чем отличаются http и https модули?
- **http** – работает по протоколу HTTP, не требует SSL/TLS.
- **https** – использует шифрование SSL/TLS, требует сертификаты.

// HTTPS сервер с SSL
const https = require('https');
const fs = require('fs');

const options = {
    key: fs.readFileSync('key.pem'),
    cert: fs.readFileSync('cert.pem')
};

const server = https.createServer(options, (req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, HTTPS!');
});

server.listen(443, () => {
    console.log('HTTPS сервер запущен');
});

Как обрабатывать POST-запросы в Node.js?
POST-запросы передают данные в теле запроса, их можно обработать через `req.on('data')`.

const http = require('http');

const server = http.createServer((req, res) => {
    if (req.method === 'POST') {
        let body = '';

        req.on('data', chunk => {
            body += chunk.toString();
        });

        req.on('end', () => {
            console.log('Полученные данные:', body);
            res.writeHead(200, { 'Content-Type': 'text/plain' });
            res.end('Данные получены');
        });
    } else {
        res.writeHead(405, { 'Content-Type': 'text/plain' });
        res.end('Метод не поддерживается');
    }
});

server.listen(3000, () => console.log('Сервер запущен на порту 3000'));

Как парсить query parameters и body запроса?
Query параметры можно разбирать с помощью встроенного модуля `url`, а тело запроса – с помощью `req.on('data')`.

const http = require('http');
const url = require('url');

const server = http.createServer((req, res) => {
    const parsedUrl = url.parse(req.url, true); // Разбор URL с query параметрами
    console.log(parsedUrl.query); // Вывод query параметров

    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ message: 'OK', query: parsedUrl.query }));
});

server.listen(3000, () => console.log('Сервер запущен на порту 3000'));

HTTP-сервер в Node.js можно легко развернуть с использованием встроенного модуля `http`, обрабатывать запросы и передавать данные клиенту.
 
Express.js
Express.js – это минималистичный и гибкий фреймворк для Node.js, который упрощает создание веб-приложений и API.
Как работает Express.js?
Express.js предоставляет удобный способ обработки HTTP-запросов, маршрутизации, работы с middleware и шаблонизации.

// Установка Express
npm install express

// Простейший сервер на Express.js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Привет, Express.js!');
});

app.listen(3000, () => console.log('Сервер запущен на http://localhost:3000'));

Чем отличается app.use() от app.get() и app.post()? 
- `app.get('/route', callback)` – обрабатывает только GET-запросы.
- `app.post('/route', callback)` – обрабатывает только POST-запросы.
- `app.use(middleware)` – применяется ко всем запросам, независимо от метода.

// Middleware для логирования
app.use((req, res, next) => {
    console.log(`Запрос ${req.method} на ${req.url}`);
    next();
});

// Обработчик GET-запроса
app.get('/hello', (req, res) => {
    res.send('Привет!');
});

// Обработчик POST-запроса
app.post('/data', (req, res) => {
    res.send('Данные получены');
});

Как работают middleware в Express?
Middleware – это функции, которые обрабатывают запросы перед их передачей в конечные маршруты.
Они могут изменять запрос, добавлять логику и выполнять аутентификацию.

// Middleware для проверки авторизации
const authMiddleware = (req, res, next) => {
    if (!req.headers.authorization) {
        return res.status(403).send('Доступ запрещён');
    }
    next();
};

// Применяем middleware к маршруту
app.get('/secure', authMiddleware, (req, res) => {
    res.send('Защищённая страница');
});

Как обрабатывать ошибки в Express?
В Express.js можно использовать специальный middleware для обработки ошибок.

// Обработчик ошибок
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Ошибка на сервере');
});

Как организовать маршрутизацию в Express?
Маршруты можно организовать с помощью `express.Router()` для структурирования кода.

// routes/userRoutes.js
const express = require('express');
const router = express.Router();

router.get('/profile', (req, res) => {
    res.send('Профиль пользователя');
});

module.exports = router;

// В главном файле
const userRoutes = require('./routes/userRoutes');
app.use('/user', userRoutes);

Express.js – это мощный инструмент для создания веб-приложений и API, который упрощает работу с маршрутизацией, middleware и обработкой ошибок.
 
Работа с базами данных в Node.js
Node.js поддерживает работу с различными базами данных, включая SQL (PostgreSQL, MySQL) и NoSQL (MongoDB). Для удобства используются ORM и библиотеки для взаимодействия с базами.
Как подключиться к MongoDB в Node.js?
Для работы с MongoDB используется библиотека `mongoose`, которая предоставляет удобный API для взаимодействия с базой.

// Установка mongoose
npm install mongoose

// Подключение к MongoDB
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log('Подключено к MongoDB'))
    .catch(err => console.error('Ошибка подключения:', err));

Как работать с PostgreSQL/MySQL через Sequelize?
Sequelize – это ORM для работы с SQL-базами, такими как PostgreSQL и MySQL.

// Установка Sequelize и драйвера для PostgreSQL
npm install sequelize pg pg-hstore

// Подключение к PostgreSQL
const { Sequelize } = require('sequelize');
const sequelize = new Sequelize('database', 'username', 'password', {
    host: 'localhost',
    dialect: 'postgres'
});

// Проверка подключения
sequelize.authenticate()
    .then(() => console.log('Подключение к базе данных успешно'))
    .catch(err => console.error('Ошибка подключения:', err));

Чем отличается SQL от NoSQL?
- **SQL (реляционные базы данных)** – данные хранятся в таблицах, строгая структура (PostgreSQL, MySQL).
- **NoSQL (нереляционные базы данных)** – данные хранятся в виде документов или ключ-значение (MongoDB, Redis).
Как правильно организовать ORM и Migrations?
ORM (Object-Relational Mapping) упрощает работу с базами данных, а миграции позволяют управлять изменениями схемы.

// Генерация модели в Sequelize
const User = sequelize.define('User', {
    username: { type: Sequelize.STRING, allowNull: false },
    email: { type: Sequelize.STRING, allowNull: false, unique: true }
});

// Создание таблицы, если её нет
sequelize.sync();

Node.js поддерживает работу с различными базами данных, а использование ORM, таких как Mongoose и Sequelize, упрощает управление данными.
 
Асинхронность в Node.js
Node.js использует асинхронную модель ввода-вывода, что позволяет выполнять операции без блокировки основного потока.
Чем callback отличается от Promise?
- **Callback** – функция, передаваемая в другую функцию и выполняемая после завершения операции.
- **Promise** – объект, который представляет будущий результат асинхронной операции и упрощает обработку ошибок.

// Callback
function fetchData(callback) {
    setTimeout(() => {
        callback('Данные загружены');
    }, 1000);
}

fetchData(data => console.log(data)); // "Данные загружены"

// Promise
function fetchDataPromise() {
    return new Promise(resolve => {
        setTimeout(() => resolve('Данные загружены'), 1000);
    });
}

fetchDataPromise().then(data => console.log(data)); // "Данные загружены"

Как работает async/await в Node.js?
`async/await` – это синтаксический сахар над `Promise`, который делает код более читаемым и понятным.

// Асинхронная функция
async function fetchData() {
    return 'Данные загружены';
}

fetchData().then(console.log); // "Данные загружены"

// Пример с ожиданием ответа
async function fetchAsyncData() {
    const data = await fetchDataPromise();
    console.log(data); // "Данные загружены"
}

fetchAsyncData();

Что такое EventEmitter и как его использовать?
В Node.js используется `EventEmitter` для обработки событий. Он позволяет реализовать подписку и обработку событий внутри приложения.

const EventEmitter = require('events');
const eventEmitter = new EventEmitter();

// Подписка на событие
eventEmitter.on('dataReceived', () => {
    console.log('Данные получены!');
});

// Генерация события
eventEmitter.emit('dataReceived');

Как process.nextTick() отличается от setImmediate()?
- `process.nextTick()` выполняет код сразу после текущего блока исполнения, до обработки других задач в event loop.
- `setImmediate()` выполняет код в следующем цикле event loop, после выполнения всех `I/O` операций.

console.log('Начало');

process.nextTick(() => console.log('nextTick'));
setImmediate(() => console.log('setImmediate'));

console.log('Конец');

// Вывод:
// Начало
// Конец
// nextTick
// setImmediate

Асинхронность в Node.js реализуется через `callbacks`, `Promise`, `async/await`, `EventEmitter` и механизмы управления очередями задач (`nextTick`, `setImmediate`).
 
Оптимизация и производительность в Node.js
Оптимизация производительности в Node.js помогает ускорить выполнение кода, уменьшить задержки и снизить нагрузку на сервер.
Как профилировать код в Node.js?
Node.js предоставляет инструменты для профилирования, такие как `console.time()`, `performance.now()`, а также внешние инструменты (`clinic.js`, `node --prof`).

// Использование console.time()
console.time('Execution Time');

setTimeout(() => {
    console.timeEnd('Execution Time');
}, 1000);

// Использование performance.now()
const { performance } = require('perf_hooks');
const start = performance.now();

// Некоторая операция
for (let i = 0; i < 1e6; i++) {}

const end = performance.now();
console.log(`Время выполнения: ${end - start} мс`);

Как использовать Cluster API для масштабирования?
Cluster API позволяет использовать все ядра процессора, создавая несколько процессов Node.js.

const cluster = require('cluster');
const http = require('http');
const os = require('os');

if (cluster.isMaster) {
    const numCPUs = os.cpus().length;
    console.log(`Форк процессов: ${numCPUs}`);

    for (let i = 0; i < numCPUs; i++) {
        cluster.fork();
    }

    cluster.on('exit', (worker) => {
        console.log(`Процесс ${worker.process.pid} завершился`);
        cluster.fork();
    });
} else {
    http.createServer((req, res) => {
        res.writeHead(200);
        res.end('Привет от сервера!');
    }).listen(8000);

    console.log(`Запущен сервер на процессе ${process.pid}`);
}

Как работают Worker Threads и когда их использовать?
Worker Threads позволяют запускать многопоточные задачи в Node.js, что полезно для CPU-интенсивных операций.

const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
    const worker = new Worker(__filename);
    worker.on('message', msg => console.log('Сообщение от воркера:', msg));
} else {
    parentPort.postMessage('Привет из воркера');
}

В чем разница между fork(), spawn() и exec()?
- `fork()` – создает новый процесс с отдельным V8-движком, подходит для IPC.
- `spawn()` – запускает новый процесс, используя системные команды.
- `exec()` – выполняет команду и буферизует вывод.

const { spawn, exec, fork } = require('child_process');

// spawn
const ls = spawn('ls', ['-lh', '/usr']);
ls.stdout.on('data', data => console.log(`Вывод: ${data}`));

// exec
exec('ls -lh /usr', (error, stdout) => console.log(stdout));

// fork
const child = fork('child.js');
child.send('Привет, дочерний процесс!');

Оптимизация Node.js включает профилирование, использование Cluster API, Worker Threads и эффективное управление процессами.
 
Безопасность в Node.js
Безопасность в Node.js важна для защиты данных, предотвращения атак и обеспечения надежной работы серверных приложений.
Как защитить API от SQL-инъекций?
SQL-инъекции позволяют злоумышленнику выполнять произвольные SQL-запросы через входные данные.
Способы защиты:
- Использование **подготовленных SQL-запросов (Prepared Statements)**.
- Валидация и экранирование пользовательского ввода.
- Использование ORM (Sequelize, Prisma).

// Использование подготовленного запроса в PostgreSQL (pg)
const { Client } = require('pg');
const client = new Client();

async function getUser(username) {
    const query = "SELECT * FROM users WHERE username = $1";
    const result = await client.query(query, [username]);
    return result.rows;
}

Как предотвратить NoSQL-инъекции?
NoSQL-инъекции возможны в MongoDB, если передавать в запросы непроверенные данные.
Способы защиты:
- Использование `sanitize` для очистки данных.
- Использование `ObjectId` вместо строк в запросах.
- Ограничение прав доступа к базе данных.

// Опасный код (уязвим для NoSQL-инъекций)
db.users.find({ username: req.body.username });

// Безопасный код
db.users.find({ username: sanitize(req.body.username) });

Что такое Helmet.js и как он защищает приложение?
Helmet.js – это middleware для Express.js, который добавляет заголовки безопасности.

// Установка Helmet.js
npm install helmet

// Использование Helmet в Express
const helmet = require('helmet');
app.use(helmet());

Как использовать JWT для аутентификации?
JWT (JSON Web Token) используется для аутентификации пользователей и защиты API.

// Создание JWT-токена (Node.js)
const jwt = require('jsonwebtoken');
const token = jwt.sign({ userId: 123 }, "SECRET_KEY", { expiresIn: '1h' });

// Проверка токена в Express.js
const authMiddleware = (req, res, next) => {
    const token = req.headers.authorization?.split(" ")[1];
    if (!token) return res.status(401).send("Нет доступа");

    try {
        const decoded = jwt.verify(token, "SECRET_KEY");
        req.user = decoded;
        next();
    } catch {
        res.status(403).send("Недействительный токен");
    }
};

Защита Node.js-приложений включает предотвращение SQL- и NoSQL-инъекций, использование Helmet.js и безопасную работу с JWT.
 
Развёртывание и DevOps для Node.js
Развёртывание Node.js-приложений включает управление процессами, контейнеризацию, развёртывание в облаке и настройку CI/CD.
Как запустить Node.js-приложение с помощью PM2?
PM2 – это процесс-менеджер для Node.js, который управляет запуском и перезапуском приложений.

// Установка PM2
npm install -g pm2

// Запуск приложения
pm2 start app.js

// Перезапуск после изменений
pm2 restart app

// Просмотр запущенных процессов
pm2 list

// Автозапуск при перезагрузке сервера
pm2 startup
pm2 save

Как контейнеризировать приложение с Docker?
Docker позволяет упаковать приложение и его зависимости в контейнер для удобного развертывания.

// Dockerfile для Node.js
FROM node:16

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

CMD ["node", "app.js"]
EXPOSE 3000


// Команды для сборки и запуска контейнера
docker build -t my-node-app .
docker run -p 3000:3000 my-node-app

Как развернуть приложение на AWS / DigitalOcean?
Для развёртывания можно использовать AWS EC2, Elastic Beanstalk, DigitalOcean Droplets или Kubernetes.
Основные шаги развертывания:
1. Установить Node.js и npm на сервере.
2. Скопировать код с помощью `scp` или `git pull`.
3. Установить зависимости `npm install`.
4. Запустить процесс через PM2 или Docker.

// Копирование проекта на сервер
scp -r ./my-project user@server-ip:/home/user/my-project

// Установка зависимостей
ssh user@server-ip "cd my-project && npm install"

// Запуск через PM2
ssh user@server-ip "pm2 start app.js"

Как настраивать CI/CD для Node.js?
CI/CD (Continuous Integration/Continuous Deployment) автоматизирует тестирование и развертывание кода.
Пример конфигурации для GitHub Actions:

name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Клонирование репозитория
        uses: actions/checkout@v2

      - name: Установка Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16'

      - name: Установка зависимостей
        run: npm install

      - name: Запуск тестов
        run: npm test

      - name: Деплой на сервер
        run: |
          scp -r . user@server-ip:/home/user/app
          ssh user@server-ip "cd /home/user/app && pm2 restart all"

Развёртывание Node.js-приложений можно автоматизировать с помощью PM2, Docker и CI/CD-пайплайнов, что повышает стабильность и масштабируемость проекта.
Express.js
Вопросы по Express.js
На собеседованиях по Express.js часто задают вопросы, связанные с основами фреймворка, маршрутизацией, middleware, обработкой ошибок, аутентификацией и развертыванием.
Что такое Express.js и какие его преимущества?
Express.js – это минималистичный и гибкий веб-фреймворк для Node.js, который упрощает создание серверных приложений и API.
Преимущества Express.js:
- Простота и минимализм.
- Гибкость и настройка middleware.
- Поддержка маршрутизации и шаблонизации.
- Интеграция с базами данных и аутентификацией.

// Простейший сервер на Express.js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Привет, Express.js!');
});

app.listen(3000, () => console.log('Сервер запущен на http://localhost:3000'));

Как работает маршрутизация в Express.js?
Маршрутизация в Express.js позволяет обрабатывать различные URL-запросы с разными HTTP-методами.

// Настройка маршрутов в Express.js
const express = require('express');
const app = express();

app.get('/user/:id', (req, res) => {
    res.send(`Пользователь с ID: ${req.params.id}`);
});

app.post('/user', (req, res) => {
    res.send('Создан новый пользователь');
});

app.listen(3000, () => console.log('Сервер запущен'));

Как работают middleware в Express.js?
Middleware – это функции, которые выполняются между запросом и ответом. Они могут изменять запрос, проверять аутентификацию, логировать данные и многое другое.

// Пример middleware в Express.js
const express = require('express');
const app = express();

app.use((req, res, next) => {
    console.log(`Запрос: ${req.method} ${req.url}`);
    next();
});

app.get('/', (req, res) => {
    res.send('Привет, Express.js!');
});

app.listen(3000, () => console.log('Сервер запущен'));

Как обработать ошибки в Express.js?
Express.js поддерживает централизованную обработку ошибок с помощью middleware-функции, принимающей 4 параметра (`err, req, res, next`).

// Глобальный обработчик ошибок в Express.js
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Ошибка на сервере!');
});
s
Как работать с CORS в Express.js?
CORS (Cross-Origin Resource Sharing) позволяет API принимать запросы с других доменов.

// Подключение CORS в Express.js
const cors = require('cors');
app.use(cors());

Как использовать JWT для аутентификации в Express.js?
JWT (JSON Web Token) используется для аутентификации пользователей и защиты API.

// Генерация JWT-токена (Node.js)
const jwt = require('jsonwebtoken');
const token = jwt.sign({ userId: 123 }, "SECRET_KEY", { expiresIn: '1h' });

// Проверка токена в Express.js
const authMiddleware = (req, res, next) => {
    const token = req.headers.authorization?.split(" ")[1];
    if (!token) return res.status(401).send("Нет доступа");

    try {
        const decoded = jwt.verify(token, "SECRET_KEY");
        req.user = decoded;
        next();
    } catch {
        res.status(403).send("Недействительный токен");
    }
};

Express.js – это удобный и гибкий фреймворк для создания веб-приложений и API. Знание маршрутизации, middleware, обработки ошибок и аутентификации поможет успешно пройти собеседование.
 
Маршрутизация (Routing) в Express.js
Маршрутизация в Express.js позволяет направлять HTTP-запросы к нужным обработчикам. Она поддерживает динамические маршруты, параметры, query-параметры и группировку маршрутов.
Как настроить маршруты в Express.js?
В Express.js маршруты задаются с использованием методов `app.get()`, `app.post()`, `app.put()`, `app.delete()` и других.

// Пример маршрутов в Express.js
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Главная страница'));
app.post('/submit', (req, res) => res.send('Данные отправлены'));
app.put('/update', (req, res) => res.send('Данные обновлены'));
app.delete('/delete', (req, res) => res.send('Данные удалены'));

app.listen(3000, () => console.log('Сервер работает на порту 3000'));

Как работает express.Router()?
`express.Router()` позволяет группировать маршруты в отдельные файлы, что улучшает структуру кода.

// routes/userRoutes.js
const express = require('express');
const router = express.Router();

router.get('/profile', (req, res) => {
    res.send('Профиль пользователя');
});

router.post('/login', (req, res) => {
    res.send('Вход выполнен');
});

module.exports = router;

// Использование в основном файле
const userRoutes = require('./routes/userRoutes');
app.use('/user', userRoutes);

Как передавать параметры в URL (req.params)?
В Express.js можно передавать параметры в маршрутах через `req.params`, используя `:` перед именем параметра.

// Пример маршрута с параметром ID
app.get('/user/:id', (req, res) => {
    res.send(`Пользователь с ID: ${req.params.id}`);
});

Как работать с query-параметрами (req.query)?
Query-параметры передаются в URL после `?` и могут быть получены через `req.query`.

// Пример обработки query-параметров
app.get('/search', (req, res) => {
    res.send(`Поиск по запросу: ${req.query.q}`);
});

// Запрос: GET /search?q=express
// Ответ: Поиск по запросу: express

Маршрутизация в Express.js позволяет управлять URL-запросами, использовать динамические параметры, query-параметры и структурировать код с помощью `express.Router()`.
 
Middleware в Express.js
Middleware – это промежуточные функции, которые выполняются во время обработки запроса. Они могут изменять запрос (`req`), ответ (`res`) и передавать управление дальше через `next()`.
Что такое middleware и как они работают?
Middleware – это функции, которые выполняются перед обработкой запроса конечным маршрутом. Они могут использоваться для логирования, обработки данных, аутентификации и других задач.

// Пример middleware в Express.js
const express = require('express');
const app = express();

// Логирование запросов
app.use((req, res, next) => {
    console.log(`Запрос: ${req.method} ${req.url}`);
    next(); // Передача управления следующему middleware
});

app.get('/', (req, res) => {
    res.send('Привет, Express.js!');
});

app.listen(3000, () => console.log('Сервер запущен на порту 3000'));

В каких случаях использовать next()?
Функция `next()` передает управление следующему middleware. Без `next()` запрос может зависнуть и не получить ответ.

// Пример использования next()
app.use((req, res, next) => {
    console.log('Middleware 1');
    next(); // Передаем управление дальше
});

app.use((req, res, next) => {
    console.log('Middleware 2');
    res.send('Ответ от сервера');
});

// Без next() Middleware 2 не выполнится

Чем отличаются глобальные и локальные middleware?
- **Глобальные middleware** – применяются ко всем запросам (`app.use()`).
- **Локальные middleware** – применяются только к определенным маршрутам.

// Глобальное middleware (для всех маршрутов)
app.use((req, res, next) => {
    console.log('Глобальный middleware');
    next();
});

// Локальное middleware (только для /secure)
const authMiddleware = (req, res, next) => {
    if (!req.headers.authorization) {
        return res.status(403).send('Доступ запрещён');
    }
    next();
};

app.get('/secure', authMiddleware, (req, res) => {
    res.send('Защищённая страница');
});

Как написать кастомный middleware?
Кастомные middleware создаются как обычные функции с параметрами `(req, res, next)`. Их можно использовать для логирования, проверки токенов, обработки данных и т. д.

// Кастомный middleware для логирования
const logger = (req, res, next) => {
    console.log(`Запрос: ${req.method} ${req.url} - ${new Date().toISOString()}`);
    next();
};

// Подключаем middleware
app.use(logger);

app.get('/', (req, res) => {
    res.send('Привет, Express.js!');
});

Middleware в Express.js позволяют выполнять промежуточную обработку запросов, например, логирование, аутентификацию, проверку прав доступа и обработку данных.
 
Работа с запросами и ответами в Express.js
Express.js позволяет легко обрабатывать входящие HTTP-запросы и отправлять ответы. Можно получать данные из URL, тела запроса, заголовков и файлов.
Как получить данные из тела запроса (req.body)?
Для работы с `req.body` в Express.js используется встроенный middleware `express.json()`.

// Подключаем middleware для обработки JSON
const express = require('express');
const app = express();

app.use(express.json());

app.post('/data', (req, res) => {
    console.log(req.body);
    res.send('Данные получены');
});

app.listen(3000, () => console.log('Сервер запущен'));

Как передавать JSON-ответы (res.json())?
Метод `res.json()` позволяет отправлять JSON-данные клиенту.

// Отправка JSON-ответа
app.get('/user', (req, res) => {
    res.json({ id: 1, name: 'Alice' });
});

Как работать с заголовками запроса?
Заголовки запроса можно получать через `req.headers` и отправлять через `res.set()`.

// Получение заголовков запроса
app.get('/headers', (req, res) => {
    console.log(req.headers);
    res.send('Заголовки получены');
});

// Установка заголовка ответа
app.get('/custom-header', (req, res) => {
    res.set('X-Custom-Header', 'Express.js');
    res.send('Заголовок установлен');
});

Как работать с файлами в Express.js?
Для загрузки файлов в Express.js используется `multer`, а для отправки файлов — `res.sendFile()`.

// Установка multer
npm install multer

// Загрузка файлов с помощью multer
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });

app.post('/upload', upload.single('file'), (req, res) => {
    res.send('Файл загружен');
});

// Отправка файла клиенту
app.get('/download', (req, res) => {
    res.sendFile(__dirname + '/example.txt');
});

Express.js позволяет удобно получать данные запроса, работать с заголовками, передавать JSON-ответы и загружать/скачивать файлы.
 
Обработка ошибок в Express.js
Обработка ошибок в Express.js позволяет предотвратить неожиданные сбои приложения и отправлять корректные ответы клиенту. Express поддерживает специальные middleware для обработки ошибок.
Как правильно обрабатывать ошибки в Express.js?
Express.js позволяет перехватывать ошибки с помощью middleware, принимающего четыре аргумента: `(err, req, res, next)`.

// Пример глобального обработчика ошибок
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ message: 'Ошибка сервера' });
});

Как создать глобальный обработчик ошибок?
Глобальный обработчик ошибок должен быть подключен в конце всех маршрутов и middleware.

// Пример глобального обработчика
app.use((err, req, res, next) => {
    res.status(err.status || 500).json({ error: err.message || 'Ошибка сервера' });
});

Как использовать next(error)?
Функция `next(error)` позволяет передавать ошибку в следующий middleware для обработки.

// Передача ошибки в next()
app.get('/error', (req, res, next) => {
    const err = new Error('Ошибка запроса');
    err.status = 400;
    next(err);
});

Обработка ошибок в Express.js позволяет поддерживать стабильную работу сервера и грамотно передавать ошибки клиентам.
 
Работа с базами данных в Express.js
Express.js позволяет работать с различными базами данных, такими как SQL (PostgreSQL, MySQL) и NoSQL (MongoDB). Для удобства используются библиотеки и ORM.
Как подключить MongoDB в Express.js?
Для работы с MongoDB в Express.js часто используется `mongoose`, который упрощает работу с базой данных.

// Установка Mongoose
npm install mongoose

// Подключение к MongoDB
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log('Подключено к MongoDB'))
    .catch(err => console.error('Ошибка подключения:', err));

Как работать с PostgreSQL/MySQL через Sequelize?
Sequelize – это ORM для работы с SQL-базами данных (PostgreSQL, MySQL).

// Установка Sequelize и драйвера PostgreSQL
npm install sequelize pg pg-hstore

// Подключение к базе данных
const { Sequelize } = require('sequelize');
const sequelize = new Sequelize('database', 'username', 'password', {
    host: 'localhost',
    dialect: 'postgres'
});

// Проверка подключения
sequelize.authenticate()
    .then(() => console.log('Подключение к базе данных успешно'))
    .catch(err => console.error('Ошибка подключения:', err));

Как защитить базу данных от SQL-инъекций?
SQL-инъекции позволяют злоумышленникам выполнять вредоносные SQL-запросы. Защита включает использование `Prepared Statements` и ORM.

// Использование подготовленного запроса (pg)
const { Client } = require('pg');
const client = new Client();

async function getUser(username) {
    const query = "SELECT * FROM users WHERE username = $1";
    const result = await client.query(query, [username]);
    return result.rows;
}

Express.js поддерживает работу с различными базами данных, а использование ORM, таких как Mongoose и Sequelize, упрощает управление данными и повышает безопасность.
 
Аутентификация и безопасность в Express.js
Аутентификация и безопасность в Express.js включают защиту API, управление пользователями и предотвращение атак (XSS, CSRF, SQL-инъекции).
Как реализовать JWT-аутентификацию в Express.js?
JWT (JSON Web Token) используется для аутентификации пользователей. Токены хранят информацию о пользователе и передаются в заголовках запроса.

// Установка библиотеки JSON Web Token
npm install jsonwebtoken

// Генерация JWT-токена
const jwt = require('jsonwebtoken');

app.post('/login', (req, res) => {
    const user = { id: 1, username: 'test' };
    const token = jwt.sign(user, 'SECRET_KEY', { expiresIn: '1h' });
    res.json({ token });
});

// Middleware для проверки JWT
const authMiddleware = (req, res, next) => {
    const token = req.headers.authorization?.split(' ')[1];
    if (!token) return res.status(401).send('Доступ запрещён');

    try {
        const decoded = jwt.verify(token, 'SECRET_KEY');
        req.user = decoded;
        next();
    } catch {
        res.status(403).send('Недействительный токен');
    }
};

// Применение middleware к защищённым маршрутам
app.get('/protected', authMiddleware, (req, res) => {
    res.send(`Привет, ${req.user.username}!`);
});

Как настроить сессии и cookies в Express.js?
Для хранения сессий и cookies в Express.js используется `express-session` и `cookie-parser`.

// Установка зависимостей
npm install express-session cookie-parser

// Подключение middleware
const session = require('express-session');
const cookieParser = require('cookie-parser');

app.use(cookieParser());
app.use(session({
    secret: 'mysecret',
    resave: false,
    saveUninitialized: true,
    cookie: { secure: false } // true для HTTPS
}));

app.get('/set-session', (req, res) => {
    req.session.user = 'TestUser';
    res.send('Сессия установлена');
});

app.get('/get-session', (req, res) => {
    res.send(`Сессия пользователя: ${req.session.user}`);
});

Как защитить API от CSRF-атак?
CSRF (Cross-Site Request Forgery) – атака, при которой злоумышленник выполняет запросы от имени пользователя. Для защиты используется `csurf`.

// Установка csurf
npm install csurf

// Подключение защиты от CSRF
const csrf = require('csurf');
const csrfProtection = csrf({ cookie: true });

app.use(csrfProtection);

app.get('/form', (req, res) => {
    res.send(`CSRF-токен: ${req.csrfToken()}`);
});

Как использовать Helmet.js для безопасности?
Helmet.js добавляет заголовки безопасности для защиты от XSS, кликджекинга и других атак.

// Установка Helmet.js
npm install helmet

// Подключение Helmet в Express
const helmet = require('helmet');
app.use(helmet());

Аутентификация и безопасность в Express.js включают JWT, управление сессиями, защиту от CSRF и использование Helmet.js для защиты заголовков.
 
Оптимизация и производительность в Express.js
Оптимизация производительности в Express.js помогает ускорить обработку запросов, уменьшить нагрузку на сервер и снизить время ответа API.
Как настроить кеширование в Express.js?
Кеширование позволяет уменьшить количество повторяющихся запросов к серверу, ускоряя обработку данных.

// Простое кеширование с использованием memory-cache
npm install memory-cache

const cache = require('memory-cache');

app.get('/data', (req, res) => {
    let cachedData = cache.get('key');
    if (cachedData) {
        return res.json(cachedData);
    }

    const newData = { message: 'Данные с сервера' };
    cache.put('key', newData, 10000); // Кешируем на 10 секунд
    res.json(newData);
});

Как использовать Compression для сжатия данных?
Сжатие HTTP-ответов уменьшает размер передаваемых данных и ускоряет загрузку.

// Установка compression
npm install compression

// Подключение middleware compression
const compression = require('compression');
app.use(compression());

app.get('/large-data', (req, res) => {
    res.json({ message: 'Большие данные', data: Array(1000).fill('данные') });
});

Как оптимизировать обработку запросов в Express.js?
Оптимизация запросов включает в себя ограничение количества запросов, использование `async/await` и минимизацию логирования в продакшене.

// Ограничение количества запросов с express-rate-limit
npm install express-rate-limit

const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 минут
    max: 100 // Максимум 100 запросов за 15 минут
});

app.use(limiter);

Как использовать Load Balancing для масштабирования?
Использование балансировки нагрузки позволяет равномерно распределять трафик между серверами.

// Запуск нескольких процессов с PM2
npm install -g pm2

// Запуск приложения в режиме кластера
pm2 start app.js -i max

// Просмотр запущенных процессов
pm2 list

Оптимизация Express.js включает кеширование, сжатие данных, ограничение запросов и балансировку нагрузки.
 
Развёртывание Express.js-приложений
Развёртывание Express.js-приложений включает управление процессами, контейнеризацию, развёртывание в облаке и настройку CI/CD.
Как запустить Express.js-приложение с помощью PM2?
PM2 – это процесс-менеджер для Node.js, который управляет запуском и перезапуском приложений.

// Установка PM2
npm install -g pm2

// Запуск Express.js-приложения
pm2 start app.js

// Перезапуск после изменений
pm2 restart app

// Просмотр запущенных процессов
pm2 list

// Автозапуск при перезагрузке сервера
pm2 startup
pm2 save

Как контейнеризировать Express.js-приложение с Docker?
Docker позволяет упаковать приложение и его зависимости в контейнер для удобного развертывания.

// Dockerfile для Express.js
FROM node:16

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

CMD ["node", "app.js"]
EXPOSE 3000


// Команды для сборки и запуска контейнера
docker build -t express-app .
docker run -p 3000:3000 express-app

Как развернуть Express.js-приложение на AWS / DigitalOcean?
Для развёртывания можно использовать AWS EC2, Elastic Beanstalk, DigitalOcean Droplets или Kubernetes.
Основные шаги развертывания:
1. Установить Node.js и npm на сервере.
2. Скопировать код с помощью `scp` или `git pull`.
3. Установить зависимости `npm install`.
4. Запустить процесс через PM2 или Docker.

// Копирование проекта на сервер
scp -r ./express-app user@server-ip:/home/user/express-app

// Установка зависимостей
ssh user@server-ip "cd express-app && npm install"

// Запуск через PM2
ssh user@server-ip "pm2 start app.js"

Как настраивать CI/CD для Express.js?
CI/CD (Continuous Integration/Continuous Deployment) автоматизирует тестирование и развертывание кода.
Пример конфигурации для GitHub Actions:

name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Клонирование репозитория
        uses: actions/checkout@v2

      - name: Установка Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16'

      - name: Установка зависимостей
        run: npm install

      - name: Запуск тестов
        run: npm test

      - name: Деплой на сервер
        run: |
          scp -r . user@server-ip:/home/user/app
          ssh user@server-ip "cd /home/user/app && pm2 restart all"

Развёртывание Express.js-приложений можно автоматизировать с помощью PM2, Docker и CI/CD-пайплайнов, что повышает стабильность и масштабируемость проекта.
Nest.js: Полное руководство
Введение в Nest.js
Nest.js - это прогрессивный фреймворк для создания серверных приложений на Node.js, основанный на TypeScript. Он использует принципы ООП, SOLID и архитектурный паттерн MVC, что делает его удобным для разработки масштабируемых приложений.
Основные компоненты Nest.js
- Модули (Modules) - группируют связанные компоненты и управляют зависимостями.
- Контроллеры (Controllers) - обрабатывают HTTP-запросы и возвращают ответы.
- Сервисы (Services) - содержат бизнес-логику и используются в контроллерах.
- Провайдеры (Providers) - используются для внедрения зависимостей.
- Middleware - промежуточные обработчики запросов, выполняющиеся до контроллеров.
- Guards, Interceptors и Pipes - инструменты для управления безопасностью, логированием и валидацией данных.
Установка и настройка проекта Nest.js
Для установки и настройки нового проекта выполните следующие команды:

npm i -g @nestjs/cli  # Установка CLI
nest new my-app       # Создание нового проекта
cd my-app             # Переход в папку проекта
npm run start         # Запуск приложения

1. Модули (Modules)
Модули в Nest.js служат для организации кода и управления зависимостями. Каждое приложение должно содержать хотя бы один модуль (корневой).
Пример создания модуля:

import { Module } from '@nestjs/common';
import { UsersService } from './users.service';
import { UsersController } from './users.controller';

@Module({
  controllers: [UsersController],
  providers: [UsersService],
})
export class UsersModule {}

2. Контроллеры (Controllers)
Контроллеры обрабатывают входящие HTTP-запросы и возвращают ответы. Они определяют маршруты приложения.
Пример создания контроллера:

import { Controller, Get } from '@nestjs/common';

@Controller('users')
export class UsersController {
  @Get()
  findAll(): string {
    return 'Возвращает всех пользователей';
  }
}

3. Сервисы (Services)
Сервисы содержат бизнес-логику и управляют данными. Они используются в контроллерах и других сервисах.
Пример создания сервиса:

import { Injectable } from '@nestjs/common';

@Injectable()
export class UsersService {
  private users = ['Alice', 'Bob', 'Charlie'];

  findAll(): string[] {
    return this.users;
  }
}

4. Провайдеры (Providers)
Провайдеры используются для внедрения зависимостей. Они включают сервисы, фабрики и классы.
Пример провайдера:

import { Injectable } from '@nestjs/common';

@Injectable()
export class LoggerService {
  log(message: string) {
    console.log(message);
  }
}

5. Middleware
Middleware выполняется перед обработкой запроса в контроллере. Они могут использоваться для логирования, аутентификации и обработки CORS.
Пример middleware:

import { Injectable, NestMiddleware } from '@nestjs/common';
import { Request, Response, NextFunction } from 'express';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log(`Request... ${req.method} ${req.url}`);
    next();
  }
}

6. Guards, Interceptors и Pipes
Guards используются для авторизации, Interceptors — для изменения запросов/ответов, Pipes — для валидации данных.
Пример Guard (проверка авторизации):

import { CanActivate, ExecutionContext, Injectable } from '@nestjs/common';

@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest();
    return request.headers.authorization === 'Bearer my-secret-token';
  }
}

Пример Pipe (валидация данных):

import { PipeTransform, Injectable, ArgumentMetadata, BadRequestException } from '@nestjs/common';

@Injectable()
export class ParseIntPipe implements PipeTransform<string, number> {
  transform(value: string, metadata: ArgumentMetadata): number {
    const val = parseInt(value, 10);
    if (isNaN(val)) {
      throw new BadRequestException('Validation failed');
    }
    return val;
  }
}

Пример Interceptor (логирование времени выполнения запроса):
Interceptors позволяют изменять запросы и ответы, а также добавлять логику до и после обработки запроса. Они могут использоваться для логирования, кэширования, трансформации данных.

import { CallHandler, ExecutionContext, Injectable, NestInterceptor } from '@nestjs/common';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    console.log('Запрос получен...');
    const now = Date.now();
    return next.handle().pipe(
      tap(() => console.log(`Запрос обработан за ${Date.now() - now}ms`)),
    );
  }
}

Создание модуля в Nest.js и его назначение
Модули (Modules) в Nest.js предназначены для организации кода и управления зависимостями. Каждое приложение состоит из модулей, которые группируют связанные контроллеры, сервисы и другие компоненты.
Пример создания модуля:

import { Module } from '@nestjs/common';
import { UsersService } from './users.service';
import { UsersController } from './users.controller';

@Module({
  controllers: [UsersController],
  providers: [UsersService],
})
export class UsersModule {}

Здесь `UsersModule` объединяет контроллер (`UsersController`) и сервис (`UsersService`). Таким образом, модули помогают структурировать приложение и делают код более читаемым и масштабируемым.
Как в Nest.js реализована поддержка TypeScript?
Nest.js изначально разрабатывался с поддержкой TypeScript, что позволяет использовать строгую типизацию, интерфейсы, декораторы и другие возможности языка. Это делает код более надежным и предсказуемым.
Пример использования интерфейса в сервисе:

export interface User {
  id: number;
  name: string;
  email: string;
}

import { Injectable } from '@nestjs/common';

@Injectable()
export class UsersService {
  private users: User[] = [];

  create(user: User) {
    this.users.push(user);
  }

  findAll(): User[] {
    return this.users;
  }
}

В данном примере используется интерфейс `User`, который помогает гарантировать, что каждый объект пользователя будет соответствовать определенной структуре.
Работа с базами данных в Nest.js (TypeORM + PostgreSQL)
Nest.js поддерживает различные ORM для работы с базами данных. Одной из самых популярных является TypeORM. Она позволяет удобно работать с реляционными базами данных, такими как PostgreSQL, MySQL и другими.
1. Установка TypeORM и PostgreSQL
Для начала необходимо установить необходимые пакеты:

npm install @nestjs/typeorm typeorm pg

После установки нужно настроить подключение к базе данных в `app.module.ts`:

import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'postgres',
      host: 'localhost',
      port: 5432,
      username: 'postgres',
      password: 'password',
      database: 'mydatabase',
      autoLoadEntities: true,
      synchronize: true, // Только для разработки!
    }),
  ],
})
export class AppModule {}

2. Создание сущности (Entity)
Сущности в TypeORM представляют собой таблицы в базе данных. Они создаются с помощью декораторов `@Entity()`, `@Column()` и других.

import { Entity, Column, PrimaryGeneratedColumn } from 'typeorm';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column({ unique: true })
  email: string;
}

3. Использование репозитория для работы с БД
Для работы с базой данных используются репозитории (`Repository`). Они позволяют выполнять CRUD-операции с таблицами.

import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from './user.entity';

@Injectable()
export class UserService {
  constructor(
    @InjectRepository(User)
    private userRepository: Repository<User>,
  ) {}

  createUser(name: string, email: string) {
    const user = this.userRepository.create({ name, email });
    return this.userRepository.save(user);
  }

  findAllUsers() {
    return this.userRepository.find();
  }
}

4. Работа с миграциями в TypeORM
Миграции в TypeORM позволяют управлять структурой базы данных без потери данных. Для создания миграции необходимо выполнить команду:

npm run typeorm migration:generate -- -n CreateUsersTable

Применить миграции можно с помощью команды:

npm run typeorm migration:run

Аутентификация с JWT в Nest.js
JWT (JSON Web Token) — это стандарт для создания безопасных токенов, используемых для аутентификации и авторизации пользователей. Nest.js предоставляет встроенную поддержку JWT с помощью пакета `@nestjs/jwt`.
1. Установка необходимых пакетов
Для работы с JWT нужно установить следующие зависимости:

npm install @nestjs/jwt @nestjs/passport passport passport-jwt bcryptjs
npm install --save-dev @types/passport-jwt @types/bcryptjs

2. Создание AuthModule
Создадим `AuthModule`, который будет содержать логику аутентификации.

import { Module } from '@nestjs/common';
import { AuthService } from './auth.service';
import { AuthController } from './auth.controller';
import { UsersModule } from '../users/users.module';
import { JwtModule } from '@nestjs/jwt';
import { PassportModule } from '@nestjs/passport';
import { JwtStrategy } from './jwt.strategy';

@Module({
  imports: [
    UsersModule,
    PassportModule,
    JwtModule.register({
      secret: 'my-secret-key', // В реальном приложении используйте переменные окружения
      signOptions: { expiresIn: '1h' },
    }),
  ],
  controllers: [AuthController],
  providers: [AuthService, JwtStrategy],
})
export class AuthModule {}

3. Создание AuthService
AuthService отвечает за валидацию пользователя и создание JWT-токенов.

import { Injectable } from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';
import * as bcrypt from 'bcryptjs';

@Injectable()
export class AuthService {
  constructor(private readonly jwtService: JwtService) {}

  async validateUser(email: string, password: string, usersService): Promise<any> {
    const user = await usersService.findByEmail(email);
    if (user && await bcrypt.compare(password, user.password)) {
      const { password, ...result } = user;
      return result;
    }
    return null;
  }

  async login(user: any) {
    const payload = { email: user.email, sub: user.id };
    return {
      access_token: this.jwtService.sign(payload),
    };
  }
}

4. Создание стратегии JWT
JWT Strategy используется для проверки токена в защищенных маршрутах.

import { Injectable } from '@nestjs/common';
import { PassportStrategy } from '@nestjs/passport';
import { ExtractJwt, Strategy } from 'passport-jwt';

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      secretOrKey: 'my-secret-key',
    });
  }

  async validate(payload: any) {
    return { userId: payload.sub, email: payload.email };
  }
}

5. Использование Guard для защиты маршрутов
Для защиты маршрутов от неавторизованных пользователей можно использовать `AuthGuard`.

import { Controller, Get, Post, Body, UseGuards, Request } from '@nestjs/common';
import { AuthService } from './auth.service';
import { JwtAuthGuard } from './jwt-auth.guard';

@Controller('auth')
export class AuthController {
  constructor(private authService: AuthService) {}

  @Post('login')
  async login(@Body() body) {
    return this.authService.login(body);
  }

  @UseGuards(JwtAuthGuard)
  @Get('profile')
  getProfile(@Request() req) {
    return req.user;
  }
}

6. Создание Guard для авторизации

import { Injectable } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';

@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {}

Теперь маршруты, защищенные `@UseGuards(JwtAuthGuard)`, требуют действительного JWT-токена для доступа.
Тестирование в Nest.js
Тестирование является важной частью разработки, позволяя убедиться, что код работает корректно. Nest.js поддерживает юнит-тестирование и интеграционное тестирование с использованием `Jest`.
1. Установка Jest
Nest.js по умолчанию использует Jest. Убедитесь, что он установлен:

npm install --save-dev jest @nestjs/testing ts-jest @types/jest

2. Юнит-тестирование сервисов
Юнит-тесты проверяют отдельные модули приложения. Пример теста для `UsersService`:

import { Test, TestingModule } from '@nestjs/testing';
import { UsersService } from './users.service';

describe('UsersService', () => {
  let service: UsersService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [UsersService],
    }).compile();

    service = module.get<UsersService>(UsersService);
  });

  it('должен быть определен', () => {
    expect(service).toBeDefined();
  });

  it('должен возвращать массив пользователей', () => {
    expect(service.findAll()).toBeInstanceOf(Array);
  });
});

3. Тестирование контроллеров
Тестирование контроллеров проверяет, корректно ли они обрабатывают HTTP-запросы. Используем `@nestjs/testing` для создания тестового модуля.

import { Test, TestingModule } from '@nestjs/testing';
import { UsersController } from './users.controller';
import { UsersService } from './users.service';

describe('UsersController', () => {
  let controller: UsersController;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [UsersController],
      providers: [UsersService],
    }).compile();

    controller = module.get<UsersController>(UsersController);
  });

  it('должен быть определен', () => {
    expect(controller).toBeDefined();
  });
});

4. Интеграционное тестирование
Интеграционные тесты проверяют взаимодействие компонентов, например, через HTTP-запросы.

import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication } from '@nestjs/common';
import * as request from 'supertest';
import { AppModule } from '../src/app.module';

describe('AppController (e2e)', () => {
  let app: INestApplication;

  beforeEach(async () => {
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  it('/ (GET)', () => {
    return request(app.getHttpServer())
      .get('/')
      .expect(200)
      .expect('Hello World!');
  });
});

Микросервисы в Nest.js
Микросервисная архитектура позволяет разбивать приложение на независимые сервисы, которые взаимодействуют друг с другом. Nest.js поддерживает микросервисы через `@nestjs/microservices` и различные транспорты, такие как Redis, Kafka, NATS и gRPC.
1. Установка необходимых пакетов
Для работы с микросервисами в Nest.js установите пакет `@nestjs/microservices`:

npm install @nestjs/microservices

2. Создание микросервисного приложения
Для создания микросервиса необходимо настроить `main.ts` и указать транспорт (например, Redis).

import { NestFactory } from '@nestjs/core';
import { MicroserviceOptions, Transport } from '@nestjs/microservices';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.createMicroservice<MicroserviceOptions>(AppModule, {
    transport: Transport.REDIS,
    options: {
      host: 'localhost',
      port: 6379,
    },
  });

  await app.listen();
}
bootstrap();

3. Обработка сообщений в микросервисе
В микросервисах используются `@MessagePattern()`, чтобы обрабатывать входящие запросы.

import { Controller } from '@nestjs/common';
import { MessagePattern } from '@nestjs/microservices';

@Controller()
export class MathController {
  @MessagePattern('sum')
  sum(data: number[]): number {
    return data.reduce((a, b) => a + b, 0);
  }
}

4. Взаимодействие с микросервисом
Основное приложение может отправлять сообщения в микросервис с помощью `ClientProxy`.

import { Injectable } from '@nestjs/common';
import { ClientProxy, ClientProxyFactory, Transport } from '@nestjs/microservices';

@Injectable()
export class MathService {
  private client: ClientProxy;

  constructor() {
    this.client = ClientProxyFactory.create({
      transport: Transport.REDIS,
      options: {
        host: 'localhost',
        port: 6379,
      },
    });
  }

  async sum(data: number[]) {
    return this.client.send<number>('sum', data).toPromise();
  }
}

5. Использование микросервиса в контроллере
Теперь можно вызвать микросервис в основном приложении через контроллер.

import { Controller, Get } from '@nestjs/common';
import { MathService } from './math.service';

@Controller('math')
export class MathController {
  constructor(private readonly mathService: MathService) {}

  @Get('sum')
  async getSum(): Promise<number> {
    return this.mathService.sum([1, 2, 3, 4]);
  }
}

Таким образом, `MathService` отправляет запрос в микросервис, а тот выполняет вычисления и возвращает результат.
Задачи для собеседования по Nest.js и их решения
На собеседовании могут задать различные практические задачи, чтобы проверить знание Nest.js. Разберем несколько типичных вопросов и их решения.
1. Реализация кастомного Pipe для валидации данных
Вам нужно создать Pipe, который проверяет, что переданный параметр является положительным числом.

import { PipeTransform, Injectable, BadRequestException } from '@nestjs/common';

@Injectable()
export class PositiveIntPipe implements PipeTransform {
  transform(value: any) {
    const parsedValue = parseInt(value, 10);
    if (isNaN(parsedValue) || parsedValue <= 0) {
      throw new BadRequestException('Value must be a positive integer');
    }
    return parsedValue;
  }
}

Этот Pipe можно использовать в контроллере, например, для проверки параметра ID:

import { Controller, Get, Param, UsePipes } from '@nestjs/common';
import { PositiveIntPipe } from './positive-int.pipe';

@Controller('users')
export class UsersController {
  @Get(':id')
  @UsePipes(PositiveIntPipe)
  getUser(@Param('id') id: number) {
    return `User with ID: ${id}`;
  }
}

2. Реализация Middleware для логирования запросов
Вам нужно создать Middleware, которое логирует все входящие HTTP-запросы.

import { Injectable, NestMiddleware } from '@nestjs/common';
import { Request, Response, NextFunction } from 'express';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
    next();
  }
}

Затем зарегистрируем Middleware в `app.module.ts`:

import { Module, MiddlewareConsumer, NestModule } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';
import { UsersModule } from './users/users.module';

@Module({
  imports: [UsersModule],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes('*');
  }
}

3. Написание теста для сервиса с мокированием зависимостей
Напишите тест для сервиса `UsersService`, который использует `UserRepository`. Репозиторий должен быть мокирован.

import { Test, TestingModule } from '@nestjs/testing';
import { UsersService } from './users.service';
import { getRepositoryToken } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from './user.entity';

const mockUserRepository = () => ({
  findOne: jest.fn().mockResolvedValue({ id: 1, name: 'Test User' }),
});

describe('UsersService', () => {
  let service: UsersService;
  let repository: Repository<User>;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        UsersService,
        { provide: getRepositoryToken(User), useFactory: mockUserRepository },
      ],
    }).compile();

    service = module.get<UsersService>(UsersService);
    repository = module.get<Repository<User>>(getRepositoryToken(User));
  });

  it('должен вернуть пользователя по ID', async () => {
    const user = await service.findOne(1);
    expect(user).toEqual({ id: 1, name: 'Test User' });
    expect(repository.findOne).toHaveBeenCalledWith({ where: { id: 1 } });
  });
});

4. Реализация Guards для проверки ролей пользователей
Напишите Guard, который разрешает доступ к маршрутам только пользователям с определенной ролью.

import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';
import { Reflector } from '@nestjs/core';

@Injectable()
export class RolesGuard implements CanActivate {
  constructor(private reflector: Reflector) {}

  canActivate(context: ExecutionContext): boolean {
    const requiredRoles = this.reflector.get<string[]>('roles', context.getHandler());
    if (!requiredRoles) return true;

    const request = context.switchToHttp().getRequest();
    const user = request.user;

    return requiredRoles.some((role) => user.roles?.includes(role));
  }
}

Guard можно использовать в контроллере, добавляя роли с помощью декоратора:

import { Controller, Get, UseGuards } from '@nestjs/common';
import { RolesGuard } from './roles.guard';
import { SetMetadata } from '@nestjs/common';

export const Roles = (...roles: string[]) => SetMetadata('roles', roles);

@Controller('admin')
@UseGuards(RolesGuard)
export class AdminController {
  @Roles('admin')
  @Get()
  getAdminData() {
    return 'Admin panel data';
  }
}

Эти задачи помогут продемонстрировать знания Nest.js на собеседовании. Они охватывают основные концепции, такие как Pipes, Middleware, Guards, тестирование и работу с зависимостями.
API
Общие вопросы по API
Этот раздел охватывает базовые концепции API, которые могут быть заданы на собеседовании. Понимание этих принципов поможет в проектировании надежных API.
1. Что такое REST API, чем оно отличается от SOAP и GraphQL?
REST (Representational State Transfer) — это архитектурный стиль для взаимодействия клиент-серверных приложений. Он использует HTTP-протокол и принципы, такие как клиент-серверная архитектура, отсутствие состояния (stateless) и кеширование.
Различия между REST, SOAP и GraphQL:
- **REST API**: Использует HTTP-методы (`GET`, `POST`, `PUT`, `DELETE`). Данные передаются в JSON или XML.
- **SOAP API**: Более сложный протокол, использующий XML. Обеспечивает строгую спецификацию и безопасность.
- **GraphQL**: Позволяет клиенту запрашивать только нужные данные, избегая избыточности.
2. Что такое HTTP-методы и когда какой использовать?
Основные HTTP-методы и их назначение:
- **GET** – Запрашивает данные (например, получение списка пользователей).
- **POST** – Создает новый ресурс (например, добавление нового пользователя).
- **PUT** – Полностью обновляет ресурс (например, обновление данных пользователя).
- **PATCH** – Частично обновляет ресурс (например, изменение только email пользователя).
- **DELETE** – Удаляет ресурс.
3. Разница между PUT и PATCH?
Оба метода используются для обновления ресурсов, но разница заключается в объеме обновляемых данных:
- **PUT** заменяет весь ресурс (если не передать все поля, пропущенные значения станут `null`).
- **PATCH** обновляет только указанные поля.
Пример:

PUT /users/1
{
  "name": "John Doe",
  "email": "john@example.com"
}

PATCH /users/1
{
  "email": "newemail@example.com"
}

4. Что такое идемпотентность и какие методы HTTP являются идемпотентными?
Идемпотентность означает, что повторный вызов одного и того же запроса приведет к одному и тому же результату.
Примеры идемпотентных методов:
- **GET** – Запрос данных не изменяет состояние сервера.
- **PUT** – Заменяет ресурс, но повторные вызовы не изменяют его дополнительно.
- **DELETE** – Удаляет ресурс (повторный DELETE не вызывает ошибку, если ресурс уже удален).
5. Чем query parameters отличаются от body в HTTP-запросах?
Query параметры (`?key=value`) используются для передачи данных в строке запроса, а тело запроса (`body`) – для передачи сложных структур данных в `POST` и `PUT`.
Пример запроса с query parameters:

GET /users?age=25&country=USA

Пример запроса с body:

POST /users
{
  "name": "John Doe",
  "email": "john@example.com"
}

6. Что такое статус-коды HTTP?
Статус-коды HTTP указывают на результат обработки запроса. Вот основные категории:
- **1xx (Informational)** – Информационные сообщения.
- **2xx (Success)** – Успешные запросы (`200 OK`, `201 Created`).
- **3xx (Redirection)** – Перенаправления (`301 Moved Permanently`, `302 Found`).
- **4xx (Client Errors)** – Ошибки клиента (`400 Bad Request`, `401 Unauthorized`, `404 Not Found`).
- **5xx (Server Errors)** – Ошибки сервера (`500 Internal Server Error`).
7. Чем 401 Unauthorized отличается от 403 Forbidden?
Разница между этими кодами связана с уровнем доступа пользователя:
- **401 Unauthorized** – Пользователь не аутентифицирован (например, не передан JWT-токен).
- **403 Forbidden** – Пользователь аутентифицирован, но не имеет прав для выполнения запроса.
Пример ответа `401 Unauthorized`:

{
  "statusCode": 401,
  "message": "Unauthorized"
}

Пример ответа `403 Forbidden`:

{
  "statusCode": 403,
  "message": "Forbidden"
}

Эти вопросы помогают лучше понять основные принципы работы API, что важно для успешного собеседования и разработки реальных проектов.
API в Nest.js
Этот раздел содержит вопросы по созданию и настройке API в Nest.js, а также объясняет основные концепции REST API.
1. Как создать REST API в Nest.js?
В Nest.js REST API создается с помощью контроллеров и сервисов. Контроллеры принимают HTTP-запросы, а сервисы обрабатывают бизнес-логику.
Пример простого контроллера:

import { Controller, Get } from '@nestjs/common';

@Controller('users')
export class UsersController {
  @Get()
  findAll() {
    return [{ id: 1, name: 'John Doe' }];
  }
}

2. Как создать маршруты в контроллере?
В Nest.js маршруты создаются с помощью декораторов `@Get()`, `@Post()`, `@Put()`, `@Delete()`.
Пример REST API с разными маршрутами:

import { Controller, Get, Post, Put, Delete, Param, Body } from '@nestjs/common';

@Controller('users')
export class UsersController {
  @Get()
  findAll() {
    return 'Получить всех пользователей';
  }

  @Get(':id')
  findOne(@Param('id') id: string) {
    return `Получить пользователя с ID ${id}`;
  }

  @Post()
  create(@Body() body) {
    return `Создать пользователя с данными: ${JSON.stringify(body)}`;
  }

  @Put(':id')
  update(@Param('id') id: string, @Body() body) {
    return `Обновить пользователя ${id} с данными: ${JSON.stringify(body)}`;
  }

  @Delete(':id')
  remove(@Param('id') id: string) {
    return `Удалить пользователя с ID ${id}`;
  }
}

3. Как передавать параметры в API?
Nest.js позволяет передавать параметры разными способами: `@Param()` (параметры URL), `@Query()` (GET-параметры), `@Body()` (тело запроса).
Пример использования разных параметров:

import { Controller, Get, Query, Param, Post, Body } from '@nestjs/common';

@Controller('users')
export class UsersController {
  @Get(':id')
  getUser(@Param('id') id: string) {
    return `User ID: ${id}`;
  }

  @Get()
  searchUsers(@Query('name') name: string) {
    return `Searching for users with name: ${name}`;
  }

  @Post()
  createUser(@Body() body) {
    return `Creating user with data: ${JSON.stringify(body)}`;
  }
}

4. Как валидировать входные данные в Nest.js?
Для валидации данных в Nest.js используется пакет `class-validator`. Он позволяет автоматически проверять данные, переданные в `@Body()`.
Установка зависимостей:

npm install class-validator class-transformer

Создание DTO (Data Transfer Object) с валидацией:

import { IsString, IsEmail, IsNotEmpty } from 'class-validator';

export class CreateUserDto {
  @IsString()
  @IsNotEmpty()
  name: string;

  @IsEmail()
  email: string;
}

Использование DTO в контроллере:

import { Controller, Post, Body, UsePipes, ValidationPipe } from '@nestjs/common';
import { CreateUserDto } from './create-user.dto';

@Controller('users')
export class UsersController {
  @Post()
  @UsePipes(new ValidationPipe())
  create(@Body() createUserDto: CreateUserDto) {
    return `User created: ${JSON.stringify(createUserDto)}`;
  }
}

5. Как защитить API с помощью Guards?
Guards используются для защиты маршрутов, например, для проверки аутентификации через JWT.
Пример Guards для проверки JWT:

import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';
import { Request } from 'express';

@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest<Request>();
    return request.headers.authorization === 'Bearer my-secret-token';
  }
}

Применение Guard в контроллере:

import { Controller, Get, UseGuards } from '@nestjs/common';
import { AuthGuard } from './auth.guard';

@Controller('profile')
@UseGuards(AuthGuard)
export class ProfileController {
  @Get()
  getProfile() {
    return 'Protected profile data';
  }
}

6. Как работает Interceptors?
Interceptors позволяют изменять запросы и ответы, а также выполнять дополнительные действия, такие как логирование.
Пример Interceptor для логирования времени запроса:

import { Injectable, NestInterceptor, ExecutionContext, CallHandler } from '@nestjs/common';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    console.log('Запрос начался...');
    const now = Date.now();
    return next.handle().pipe(
      tap(() => console.log(`Запрос обработан за ${Date.now() - now}ms`)),
    );
  }
}

Применение Interceptor в контроллере:

import { Controller, Get, UseInterceptors } from '@nestjs/common';
import { LoggingInterceptor } from './logging.interceptor';

@Controller('users')
@UseInterceptors(LoggingInterceptor)
export class UsersController {
  @Get()
  findAll() {
    return 'Fetching users...';
  }
}

Этот раздел охватывает ключевые аспекты создания API в Nest.js, включая маршруты, валидацию, Guards и Interceptors.
Безопасность API в Nest.js
Безопасность API — это важный аспект разработки, позволяющий защитить данные от атак и несанкционированного доступа. В этом разделе рассматриваются ключевые методы защиты API в Nest.js.
1. Как защитить API с помощью JWT-аутентификации?
JWT (JSON Web Token) используется для аутентификации пользователей, передавая токен в заголовках запроса.
Пример настройки JWT в Nest.js:

import { Module } from '@nestjs/common';
import { JwtModule } from '@nestjs/jwt';

@Module({
  imports: [
    JwtModule.register({
      secret: 'my-secret-key', // Используйте переменные окружения
      signOptions: { expiresIn: '1h' },
    }),
  ],
})
export class AuthModule {}

Создание Guard для проверки JWT:

import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';
import { Request } from 'express';

@Injectable()
export class JwtAuthGuard implements CanActivate {
  constructor(private jwtService: JwtService) {}

  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest<Request>();
    const token = request.headers.authorization?.split(' ')[1];
    try {
      return !!this.jwtService.verify(token);
    } catch (error) {
      return false;
    }
  }
}

2. Как работает passport-jwt в Nest.js?
Nest.js поддерживает библиотеку `passport-jwt` для аутентификации. Она автоматически извлекает и проверяет JWT из заголовков запроса.
Установка необходимых пакетов:

npm install @nestjs/passport passport passport-jwt
npm install --save-dev @types/passport-jwt

Пример настройки `passport-jwt`:

import { Injectable } from '@nestjs/common';
import { PassportStrategy } from '@nestjs/passport';
import { ExtractJwt, Strategy } from 'passport-jwt';

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      secretOrKey: 'my-secret-key',
    });
  }

  async validate(payload: any) {
    return { userId: payload.sub, email: payload.email };
  }
}

3. Как настроить CORS в API?
CORS (Cross-Origin Resource Sharing) предотвращает доступ к API с неизвестных источников. В Nest.js CORS можно настроить глобально.
Пример включения CORS:

import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.enableCors(); // Включение CORS
  await app.listen(3000);
}
bootstrap();

4. Что такое CSRF и как от него защититься?
CSRF (Cross-Site Request Forgery) — это атака, при которой злоумышленник заставляет браузер жертвы выполнить нежелательный запрос от имени пользователя. В Nest.js можно использовать middleware для защиты.
Пример защиты от CSRF с `csurf`:

npm install csurf

Применение `csurf` в Nest.js:

import * as csurf from 'csurf';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.use(csurf());
  await app.listen(3000);
}
bootstrap();

5. Как предотвратить SQL-инъекции в Nest.js?
SQL-инъекции позволяют злоумышленникам изменять запросы к базе данных. В Nest.js рекомендуется использовать ORM (TypeORM, Prisma) или подготовленные запросы.
Пример защиты от SQL-инъекций в TypeORM:

const user = await this.userRepository.findOne({
  where: { email: email },
});

Пример использования `queryBuilder`:

const user = await this.userRepository
  .createQueryBuilder('user')
  .where('user.email = :email', { email })
  .getOne();

6. Что такое rate limiting и как его реализовать?
Rate limiting предотвращает DDoS-атаки и ограничивает число запросов от одного клиента. Для этого можно использовать `nestjs-throttler`.
Установка пакета:

npm install @nestjs/throttler

Настройка rate limiting в `app.module.ts`:

import { Module } from '@nestjs/common';
import { ThrottlerModule } from '@nestjs/throttler';

@Module({
  imports: [
    ThrottlerModule.forRoot({
      ttl: 60, // 60 секунд
      limit: 10, // Максимум 10 запросов в минуту
    }),
  ],
})
export class AppModule {}

Применение в контроллере:

import { Controller, Get, UseGuards } from '@nestjs/common';
import { ThrottlerGuard } from '@nestjs/throttler';

@Controller('users')
@UseGuards(ThrottlerGuard)
export class UsersController {
  @Get()
  findAll() {
    return 'Fetching users...';
  }
}

Безопасность API — это важный аспект разработки. Nest.js предоставляет мощные инструменты для защиты API, такие как JWT, Guards, CORS, CSRF-защита, защита от SQL-инъекций и ограничение запросов (rate limiting).
Тестирование API в Nest.js
Тестирование API в Nest.js помогает убедиться в корректной работе маршрутов, контроллеров и сервисов. В этом разделе разберем юнит-тесты, интеграционные тесты и e2e-тестирование.
1. Как тестировать API в Nest.js с Supertest?
Supertest — это библиотека для тестирования HTTP-запросов. Она позволяет отправлять запросы к API и проверять ответы.
Установка Supertest:

npm install --save-dev supertest

Пример e2e-теста с Supertest:

import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication } from '@nestjs/common';
import * as request from 'supertest';
import { AppModule } from '../src/app.module';

describe('AppController (e2e)', () => {
  let app: INestApplication;

  beforeEach(async () => {
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  it('/users (GET)', () => {
    return request(app.getHttpServer())
      .get('/users')
      .expect(200)
      .expect([]); // Ожидаемый ответ - пустой массив
  });
});

2. Как писать юнит-тесты для контроллеров?
Юнит-тестирование контроллеров позволяет проверить, правильно ли они обрабатывают HTTP-запросы.
Пример теста для `UsersController`:

import { Test, TestingModule } from '@nestjs/testing';
import { UsersController } from './users.controller';
import { UsersService } from './users.service';

describe('UsersController', () => {
  let controller: UsersController;
  let service: UsersService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [UsersController],
      providers: [UsersService],
    }).compile();

    controller = module.get<UsersController>(UsersController);
    service = module.get<UsersService>(UsersService);
  });

  it('должен быть определен', () => {
    expect(controller).toBeDefined();
  });

  it('должен возвращать пользователей', async () => {
    jest.spyOn(service, 'findAll').mockImplementation(() => ['user1', 'user2']);
    expect(controller.findAll()).toEqual(['user1', 'user2']);
  });
});

3. Как мокировать зависимости при тестировании API?
При тестировании сервисов и контроллеров часто требуется подменить реальные зависимости (репозитории, другие сервисы) на заглушки.
Пример мокирования репозитория:

import { Test, TestingModule } from '@nestjs/testing';
import { UsersService } from './users.service';
import { getRepositoryToken } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from './user.entity';

const mockUserRepository = () => ({
  findOne: jest.fn().mockResolvedValue({ id: 1, name: 'Test User' }),
});

describe('UsersService', () => {
  let service: UsersService;
  let repository: Repository<User>;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        UsersService,
        { provide: getRepositoryToken(User), useFactory: mockUserRepository },
      ],
    }).compile();

    service = module.get<UsersService>(UsersService);
    repository = module.get<Repository<User>>(getRepositoryToken(User));
  });

  it('должен вернуть пользователя по ID', async () => {
    const user = await service.findOne(1);
    expect(user).toEqual({ id: 1, name: 'Test User' });
    expect(repository.findOne).toHaveBeenCalledWith({ where: { id: 1 } });
  });
});

4. Чем интеграционные тесты отличаются от юнит-тестов?
- **Юнит-тесты** проверяют работу отдельных компонентов (контроллеров, сервисов) в изоляции.
- **Интеграционные тесты** проверяют взаимодействие между компонентами и модулями приложения.
Пример интеграционного теста:

import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication } from '@nestjs/common';
import * as request from 'supertest';
import { AppModule } from '../src/app.module';

describe('UsersModule (Integration Test)', () => {
  let app: INestApplication;

  beforeEach(async () => {
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  it('/users (GET) должно вернуть 200', async () => {
    return request(app.getHttpServer())
      .get('/users')
      .expect(200);
  });
});

Тестирование API — это важный процесс, который включает юнит-тестирование, интеграционные тесты и e2e-тестирование. Использование Jest и Supertest в Nest.js позволяет автоматизировать тестирование и улучшить надежность кода.
Документация API в Nest.js
Документирование API помогает разработчикам и пользователям понять, как взаимодействовать с сервисом. Nest.js поддерживает автоматическую генерацию документации с помощью Swagger.
1. Как документировать API с помощью Swagger?
Swagger позволяет автоматически генерировать документацию для REST API. В Nest.js для этого используется пакет `@nestjs/swagger`.
Установка Swagger в проект:

npm install --save @nestjs/swagger swagger-ui-express

Настройка Swagger в `main.ts`:

import { NestFactory } from '@nestjs/core';
import { DocumentBuilder, SwaggerModule } from '@nestjs/swagger';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('Users API')
    .setDescription('Документация API пользователей')
    .setVersion('1.0')
    .addBearerAuth() // Добавление авторизации через JWT
    .build();

  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api/docs', app, document);

  await app.listen(3000);
}
bootstrap();

2. Как добавлять описание к контроллерам и методам?
Для улучшения документации можно использовать декораторы `@ApiTags()`, `@ApiOperation()`, `@ApiResponse()`.
Пример контроллера с описаниями для Swagger:

import { Controller, Get, Post, Body } from '@nestjs/common';
import { ApiTags, ApiOperation, ApiResponse } from '@nestjs/swagger';

@ApiTags('users') // Группировка в документации
@Controller('users')
export class UsersController {
  @ApiOperation({ summary: 'Получить всех пользователей' })
  @ApiResponse({ status: 200, description: 'Список пользователей' })
  @Get()
  findAll() {
    return [{ id: 1, name: 'John Doe' }];
  }

  @ApiOperation({ summary: 'Создать нового пользователя' })
  @ApiResponse({ status: 201, description: 'Пользователь создан' })
  @Post()
  create(@Body() body) {
    return { id: 2, ...body };
  }
}

3. Как описывать DTO в документации Swagger?
Для автоматического документирования структуры входных данных можно использовать `@ApiProperty()`.
Пример DTO с Swagger-декораторами:

import { ApiProperty } from '@nestjs/swagger';

export class CreateUserDto {
  @ApiProperty({ example: 'John Doe', description: 'Имя пользователя' })
  name: string;

  @ApiProperty({ example: 'john@example.com', description: 'Email пользователя' })
  email: string;
}

Использование DTO в контроллере:

import { Controller, Post, Body } from '@nestjs/common';
import { CreateUserDto } from './create-user.dto';
import { ApiOperation, ApiResponse } from '@nestjs/swagger';

@Controller('users')
export class UsersController {
  @ApiOperation({ summary: 'Создать нового пользователя' })
  @ApiResponse({ status: 201, description: 'Пользователь успешно создан' })
  @Post()
  create(@Body() createUserDto: CreateUserDto) {
    return { id: 2, ...createUserDto };
  }
}

4. Как добавить авторизацию в документацию Swagger?
Для добавления JWT-аутентификации в Swagger используется `@ApiBearerAuth()`.
Пример контроллера с защитой API:

import { Controller, Get, UseGuards } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';
import { ApiBearerAuth, ApiOperation } from '@nestjs/swagger';

@Controller('profile')
@UseGuards(AuthGuard('jwt')) // Защита маршрута
@ApiBearerAuth() // Добавление авторизации в Swagger
export class ProfileController {
  @ApiOperation({ summary: 'Получить профиль пользователя' })
  @Get()
  getProfile() {
    return { id: 1, name: 'John Doe' };
  }
}

5. Как кастомизировать Swagger UI?
Swagger UI можно настроить, изменив цветовую схему, логотип и заголовки.
Пример кастомизации:

const config = new DocumentBuilder()
  .setTitle('Custom API')
  .setDescription('Моя кастомная документация')
  .setVersion('2.0')
  .addBearerAuth()
  .build();

6. Как экспортировать документацию в JSON?
Можно экспортировать документацию в формате JSON для использования в других сервисах.
Пример экспорта документации:

import { writeFileSync } from 'fs';

const document = SwaggerModule.createDocument(app, config);
writeFileSync('./swagger.json', JSON.stringify(document));

Документирование API с помощью Swagger помогает разработчикам быстрее понять, как использовать API. Nest.js предоставляет мощные инструменты для автоматического создания документации.
Производительность и масштабируемость API в Nest.js
При создании высоконагруженных API важно учитывать их производительность и масштабируемость. В этом разделе разберем методы оптимизации API в Nest.js.
1. Как реализовать кэширование в Nest.js?
Кэширование позволяет уменьшить нагрузку на сервер, сохраняя часто используемые данные.
Установка модуля кэширования:

npm install @nestjs/cache-manager cache-manager

Пример включения кэширования:

import { Module, CacheModule } from '@nestjs/common';

@Module({
  imports: [CacheModule.register()],
})
export class AppModule {}

Использование кэша в сервисе:

import { Injectable, CacheService } from '@nestjs/common';

@Injectable()
export class UsersService {
  constructor(private cacheService: CacheService) {}

  async getUsers() {
    const cachedUsers = await this.cacheService.get('users');
    if (cachedUsers) return cachedUsers;

    const users = [{ id: 1, name: 'John Doe' }]; // Запрос к БД
    await this.cacheService.set('users', users, { ttl: 60 });
    return users;
  }
}

2. Как использовать Redis для кэширования?
Redis — это быстрый in-memory хранилище, которое можно использовать для кэширования API.
Установка Redis и модуля для Nest.js:

npm install cache-manager-redis-store

Пример настройки Redis в `app.module.ts`:

import { CacheModule, Module } from '@nestjs/common';
import * as redisStore from 'cache-manager-redis-store';

@Module({
  imports: [
    CacheModule.register({
      store: redisStore,
      host: 'localhost',
      port: 6379,
      ttl: 60, // Время жизни кэша в секундах
    }),
  ],
})
export class AppModule {}

3. Как реализовать lazy loading модулей?
Lazy loading (ленивая загрузка) позволяет загружать модули только при необходимости, что снижает нагрузку на приложение при старте.
Пример загрузки модуля по запросу:

import { Module, DynamicModule } from '@nestjs/common';

@Module({})
export class DynamicFeatureModule {
  static register(): DynamicModule {
    return {
      module: DynamicFeatureModule,
      providers: [],
    };
  }
}

Применение в `AppModule`:

import { Module } from '@nestjs/common';
import { DynamicFeatureModule } from './dynamic-feature.module';

@Module({
  imports: [DynamicFeatureModule.register()],
})
export class AppModule {}

4. Как уменьшить размер ответа API?
Для уменьшения размера ответа можно использовать компрессию и исключение ненужных полей.
Установка компрессии:

npm install compression

Применение компрессии в `main.ts`:

import * as compression from 'compression';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.use(compression());
  await app.listen(3000);
}
bootstrap();

5. Как использовать GraphQL вместо REST API?
GraphQL позволяет запрашивать только нужные данные, снижая нагрузку на сеть.
Установка GraphQL:

npm install @nestjs/graphql graphql apollo-server-express

Пример GraphQL схемы:

import { Query, Resolver } from '@nestjs/graphql';

@Resolver()
export class UsersResolver {
  @Query(() => String)
  hello() {
    return 'Hello GraphQL';
  }
}

6. Как реализовать API versioning?
API versioning помогает управлять разными версиями API, не ломая совместимость.
Пример настройки версионности API:

import { VersioningType } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.enableVersioning({ type: VersioningType.URI });
  await app.listen(3000);
}
bootstrap();

Использование версий в контроллере:

import { Controller, Get } from '@nestjs/common';

@Controller({ path: 'users', version: '1' })
export class UsersControllerV1 {
  @Get()
  findAll() {
    return 'Users API v1';
  }
}

@Controller({ path: 'users', version: '2' })
export class UsersControllerV2 {
  @Get()
  findAll() {
    return 'Users API v2';
  }
}

Производительность и масштабируемость API — ключевой аспект разработки. Nest.js предоставляет множество инструментов, включая кэширование, Redis, lazy loading, сжатие данных и GraphQL для повышения эффективности API.
Развёртывание и документация API в Nest.js
Этот раздел охватывает процесс документирования API с помощью Swagger и развертывание Nest.js-приложения с использованием Docker и CI/CD.
1. Как документировать API с помощью Swagger?
Swagger — это инструмент для автоматической генерации документации API. Nest.js предоставляет официальный пакет `@nestjs/swagger`, который интегрируется с контроллерами.
Установка Swagger в проект:

npm install @nestjs/swagger swagger-ui-express

Настройка Swagger в `main.ts`:

import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { DocumentBuilder, SwaggerModule } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('API Documentation')
    .setDescription('Описание REST API')
    .setVersion('1.0')
    .addBearerAuth()
    .build();

  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api', app, document);

  await app.listen(3000);
}
bootstrap();

Пример использования Swagger-декораторов в контроллере:

import { Controller, Get, Post, Body } from '@nestjs/common';
import { ApiTags, ApiOperation, ApiResponse } from '@nestjs/swagger';

@ApiTags('users')
@Controller('users')
export class UsersController {
  @Get()
  @ApiOperation({ summary: 'Получить всех пользователей' })
  @ApiResponse({ status: 200, description: 'Список пользователей' })
  findAll() {
    return [{ id: 1, name: 'John Doe' }];
  }

  @Post()
  @ApiOperation({ summary: 'Создать нового пользователя' })
  @ApiResponse({ status: 201, description: 'Пользователь создан' })
  create(@Body() body) {
    return `User created: ${JSON.stringify(body)}`;
  }
}

2. Как развернуть API в Docker?
Docker позволяет контейнеризировать приложение и запускать его в любом окружении.
Создание `Dockerfile` для Nest.js-приложения:

# Используем официальный образ Node.js
FROM node:18

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем package.json и устанавливаем зависимости
COPY package*.json ./
RUN npm install

# Копируем исходный код
COPY . .

# Сборка TypeScript-кода
RUN npm run build

# Открываем порт 3000
EXPOSE 3000

# Запуск приложения
CMD ["node", "dist/main"]

Создание `docker-compose.yml` для запуска Nest.js и PostgreSQL:

version: '3.8'

services:
  postgres:
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: nestjs
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    ports:
      - '5432:5432'

  app:
    build: .
    restart: always
    depends_on:
      - postgres
    environment:
      DATABASE_URL: postgresql://nestjs:password@postgres:5432/mydatabase
    ports:
      - '3000:3000'

3. Как настроить CI/CD для Nest.js?
CI/CD (Continuous Integration / Continuous Deployment) позволяет автоматически тестировать и развёртывать приложение. В качестве примера разберём конфигурацию для GitHub Actions.
Создание `.github/workflows/deploy.yml`:

name: Deploy NestJS App

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout репозитория
        uses: actions/checkout@v3

      - name: Установка Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Установка зависимостей
        run: npm install

      - name: Запуск тестов
        run: npm run test

      - name: Сборка проекта
        run: npm run build

      - name: Деплой на сервер (пример с SSH)
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SERVER_HOST }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SERVER_SSH_KEY }}
          script: |
            cd /var/www/nestjs-app
            git pull origin main
            npm install
            npm run build
            pm2 restart all

Документирование и развёртывание API — важные этапы в разработке. Swagger позволяет создавать удобную документацию, Docker — контейнеризировать приложение, а CI/CD автоматизирует тестирование и деплой.
 
Docker: Полное руководство
1. Основы Docker
Docker — это платформа для контейнеризации приложений, позволяющая упаковать, распространять и запускать приложения в изолированных средах.
Что такое Docker и зачем он нужен?
Docker — это инструмент для контейнеризации, который позволяет запускать приложения в легковесных, изолированных средах (контейнерах). Контейнеры обеспечивают единообразие среды выполнения, что особенно полезно при развертывании.
Преимущества Docker:
- **Портативность**: Можно запускать контейнеры в любом окружении.
- **Изоляция**: Контейнеры не конфликтуют между собой.
- **Быстродействие**: Контейнеры запускаются быстрее, чем виртуальные машины.
- **Масштабируемость**: Легко управлять множеством контейнеров.
В чем разница между контейнером и виртуальной машиной?
Основное отличие заключается в том, что контейнеры используют ядро операционной системы хоста, в то время как виртуальные машины содержат свою собственную операционную систему.
Сравнение контейнера и виртуальной машины:
- **Контейнеры** используют общий хост-ОС, что делает их легче и быстрее.
- **Виртуальные машины** эмулируют оборудование, что требует больше ресурсов.
Что такое Docker Image и Docker Container?
Docker Image (образ) — это шаблон, содержащий все необходимые файлы и зависимости для запуска приложения. Контейнер — это запущенный экземпляр образа.
Пример создания контейнера из образа:

docker pull nginx        # Загружаем образ Nginx
docker run -d -p 8080:80 nginx  # Запускаем контейнер

Как создать и запустить контейнер?
Для запуска контейнера используется команда `docker run`. Можно указать параметры, такие как порты и имя контейнера.
Пример запуска контейнера:

docker run --name my-nginx -d -p 8080:80 nginx

Как посмотреть список работающих контейнеров?
Список запущенных контейнеров можно получить с помощью команды:

docker ps

Чтобы увидеть все контейнеры (включая остановленные), используйте:

docker ps -a

Как остановить или удалить контейнер?
Остановка контейнера:

docker stop my-nginx

Удаление контейнера:

docker rm my-nginx

Как посмотреть логи контейнера?
Просмотр логов выполняется с помощью команды:

docker logs my-nginx

Как работает `docker exec` и зачем он нужен?
Команда `docker exec` позволяет выполнить команду внутри работающего контейнера. Часто используется для входа в контейнер и диагностики.
Пример запуска bash в контейнере:

docker exec -it my-nginx bash

Этот раздел охватывает основные команды Docker и концепции контейнеризации. Следующим шагом можно рассмотреть работу с `Dockerfile` и созданием образов.
 
2. Dockerfile и создание образов
Dockerfile — это текстовый файл с инструкциями для сборки образа Docker. Он определяет, какие зависимости, файлы и команды нужны для создания контейнера.
Что такое Dockerfile и как он работает?
Dockerfile содержит последовательность команд, которые Docker использует для создания образа. Созданный на его основе образ можно запустить как контейнер.
Пример простого `Dockerfile`:

# Используем официальный образ Node.js
FROM node:18

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем файлы package.json и устанавливаем зависимости
COPY package*.json ./
RUN npm install

# Копируем весь код проекта
COPY . .

# Открываем порт 3000
EXPOSE 3000

# Запуск приложения
CMD ["node", "server.js"]

Как создать образ из Dockerfile?
Чтобы создать образ на основе `Dockerfile`, используйте команду:

docker build -t my-app .

Флаги:
- `-t my-app` — имя создаваемого образа.
- `.` — путь к `Dockerfile` (текущая директория).
Как уменьшить размер Docker-образа?
Основные способы уменьшения размера образа:
- **Использовать легковесные базовые образы** (например, `node:18-alpine` вместо `node:18`).
- **Удалять временные файлы после установки зависимостей.**
- **Использовать multi-stage builds** (см. ниже).
В чем разница между COPY и ADD в Dockerfile?
Оба оператора копируют файлы в контейнер, но `ADD` имеет дополнительные возможности.
Различия:
- `COPY` просто копирует файлы и папки.
- `ADD` может распаковывать архивы и загружать файлы по URL.
Пример использования `COPY` и `ADD`:

COPY myfile.txt /app/myfile.txt
ADD archive.tar.gz /app/ # Распакует архив

Что делает CMD и ENTRYPOINT, в чем разница?
Обе команды определяют, какая команда будет выполняться в контейнере по умолчанию.
Различия:
- `CMD` задает команду по умолчанию, но ее можно переопределить при запуске контейнера.
- `ENTRYPOINT` задает неизменяемую команду, которую всегда выполняет контейнер.
Пример использования:

CMD ["nginx", "-g", "daemon off;"] # Можно переопределить при запуске

ENTRYPOINT ["nginx", "-g", "daemon off;"] # Нельзя переопределить

Как передавать переменные окружения в контейнер?
Передача переменных окружения выполняется через `ENV` или `docker run -e`.
Пример использования `ENV` в `Dockerfile`:

ENV NODE_ENV=production

Передача переменных при запуске контейнера:

docker run -e NODE_ENV=production my-app

Как использовать .dockerignore?
Файл `.dockerignore` исключает ненужные файлы из сборки образа.
Пример `.dockerignore`:

node_modules
dist
.env
.DS_Store

Как оптимизировать Dockerfile для продакшена?
Для продакшена используются multi-stage builds, чтобы уменьшить размер образа.
Пример multi-stage build:

# Первый этап — сборка
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Второй этап — запуск только нужных файлов
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY package.json ./
RUN npm install --only=production
CMD ["node", "dist/main.js"]

Dockerfile позволяет автоматизировать процесс создания образов. Следующим шагом можно рассмотреть работу с Docker Hub и репозиториями.
 
3. Работа с Docker Hub и репозиториями
Docker Hub — это облачный сервис для хранения и распространения Docker-образов. Можно загружать образы в публичные или приватные репозитории и скачивать их для развертывания.
Как загрузить образ в Docker Hub?
Для загрузки образа в Docker Hub нужно войти в свою учетную запись и выполнить команду `docker push`.
1. Войти в Docker Hub:

docker login

2. Переименовать образ в формат `<username>/<repository>:tag`:

docker tag my-app myusername/my-app:latest

3. Загрузить образ в Docker Hub:

docker push myusername/my-app:latest

Как скачать образ с Docker Hub?
Для загрузки образа используется команда `docker pull`:

docker pull nginx:latest

Запуск контейнера после загрузки образа:

docker run -d -p 8080:80 nginx

Как создать приватный репозиторий в Docker Hub?
По умолчанию репозитории в Docker Hub являются публичными, но можно создать приватный репозиторий.
1. Перейти на сайт [hub.docker.com](https://hub.docker.com/).
2. В разделе **Repositories** нажать **Create Repository**.
3. Ввести имя репозитория и выбрать **Private**.
4. Использовать этот репозиторий так же, как публичный, но доступ к нему будет ограничен.
Как использовать теги (`tag`) для образов?
Docker-теги помогают управлять версиями образов. Если не указывать тег, по умолчанию используется `latest`.
Создание образа с тегом:

docker build -t my-app:v1 .

Просмотр тегов образа:

docker images my-app

Использование определенного тега при запуске контейнера:

docker run -d -p 8080:80 my-app:v1

Docker Hub позволяет удобно управлять образами и делиться ими с командой. Следующим шагом можно рассмотреть работу с Docker Compose для управления несколькими контейнерами.
 
4. Docker Compose
Docker Compose — это инструмент для управления многоконтейнерными приложениями. Позволяет описывать конфигурацию контейнеров в файле `docker-compose.yml` и запускать их одной командой.
Что такое Docker Compose и зачем он нужен?
Docker Compose используется для запуска нескольких контейнеров, которые взаимодействуют между собой. Например, приложение может состоять из **бэкенда**, **базы данных** и **кэша** (Redis), и все это можно описать в одном `docker-compose.yml`.
Как запустить несколько сервисов с `docker-compose.yml`?
Пример `docker-compose.yml` для Nest.js + PostgreSQL:

version: '3.8'

services:
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  app:
    build: .
    restart: always
    depends_on:
      - db
    environment:
      DATABASE_URL: postgres://user:password@db:5432/mydatabase
    ports:
      - "3000:3000"
    command: ["npm", "run", "start"]

volumes:
  postgres_data:

Запуск всех контейнеров одной командой:

docker-compose up -d

Как передавать переменные окружения в `docker-compose`?
Переменные окружения можно хранить в файле `.env` и загружать в `docker-compose.yml`.
Пример `.env` файла:

POSTGRES_USER=user
POSTGRES_PASSWORD=password
POSTGRES_DB=mydatabase

Использование `.env` в `docker-compose.yml`:

version: '3.8'

services:
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}

Как работает `depends_on`?
`depends_on` определяет порядок запуска контейнеров, но **не гарантирует**, что зависимый сервис полностью инициализирован перед запуском другого.
Пример использования:

services:
  db:
    image: postgres

  app:
    build: .
    depends_on:
      - db

В чем разница между `docker run` и `docker-compose up`?
Основные отличия:
- `docker run` запускает **один** контейнер.
- `docker-compose up` управляет **множеством контейнеров**, описанных в `docker-compose.yml`.
- `docker-compose` упрощает конфигурацию, позволяя использовать `.env`, `volumes` и `networks`.
Docker Compose упрощает управление сложными приложениями, состоящими из нескольких контейнеров. Следующим шагом можно рассмотреть работу с сетями Docker.
 
5. Сетевые настройки Docker
Docker предоставляет несколько типов сетей для организации взаимодействия контейнеров между собой и с внешним миром.
Какие бывают типы сетей в Docker?
Docker поддерживает следующие типы сетей:
- **Bridge (мостовая)** – стандартная сеть для связи контейнеров на одном хосте.
- **Host** – контейнер использует сеть хоста (нет изоляции портов).
- **None** – контейнер не имеет сетевого подключения.
- **Overlay** – используется в Docker Swarm для связи между хостами.
- **Macvlan** – контейнер получает свой IP-адрес в сети, как обычное устройство.
Как работает `bridge`, `host`, `none` сети?
**Bridge-сеть (по умолчанию)** – контейнеры подключаются к виртуальному мосту, что позволяет им взаимодействовать друг с другом.

docker network create my_bridge
docker run --network my_bridge nginx

**Host-сеть** – контейнер использует сеть хоста, то есть его порты совпадают с портами машины.

docker run --network host nginx

**None-сеть** – контейнер не подключен ни к одной сети, он полностью изолирован.

docker run --network none nginx

Как соединить несколько контейнеров в одной сети?
Создание сети и подключение контейнеров:

docker network create my_network

docker run -d --network my_network --name app nginx
docker run -d --network my_network --name db postgres

Теперь контейнер `app` может обращаться к `db` по его имени (`db`).
Как открыть порты в контейнере?
Чтобы открыть порт контейнера для внешнего доступа, используйте флаг `-p`.

docker run -d -p 8080:80 nginx

Здесь порт `8080` на хосте будет перенаправлен на `80` порт контейнера.
Docker предоставляет мощные возможности для сетевого взаимодействия контейнеров. Следующим шагом можно рассмотреть работу с хранилищем данных в Docker.
 
6. Хранение данных в Docker (Volumes)
Docker Volumes используются для хранения данных вне контейнера, что позволяет сохранять данные при перезапуске или обновлении контейнера.
Что такое Docker Volumes и зачем они нужны?
Docker Volumes – это механизм хранения данных вне контейнера, который позволяет:
- **Сохранять данные при перезапуске контейнера**.
- **Разделять данные между несколькими контейнерами**.
- **Уменьшить нагрузку на файловую систему контейнера**.
В чем разница между `bind mount` и `volume`?
Docker поддерживает два основных метода хранения данных:
1. **Volumes** – управляются самим Docker и хранятся в `/var/lib/docker/volumes/`.
2. **Bind mounts** – монтируются напрямую из файловой системы хоста.
Пример создания тома (`volume`):

docker volume create my_volume

Пример использования `bind mount` для монтирования локальной папки:

docker run -d -v /home/user/data:/app/data nginx

Как подключить внешний каталог к контейнеру?
Пример монтирования локальной папки `/data` внутрь контейнера:

docker run -d -v /data:/app/data nginx

Как создать и удалить том (`volume`)?
Создание тома:

docker volume create my_data

Удаление тома:

docker volume rm my_data

Просмотр всех томов:

docker volume ls

Использование Volumes – это надежный способ хранения данных в Docker. Следующим шагом можно рассмотреть вопросы безопасности контейнеров.
 
7. Безопасность в Docker
Безопасность контейнеров в Docker – важная часть DevOps. Неправильная конфигурация может привести к утечке данных и уязвимостям в системе.
Какие уязвимости бывают у контейнеров?
Основные угрозы безопасности в Docker:
- **Использование устаревших или небезопасных образов**.
- **Запуск контейнеров с привилегиями root**.
- **Открытые порты без ограничения доступа**.
- **Использование неподписанных образов**.
- **Хранение секретных данных внутри контейнеров**.
Как ограничить доступ к ресурсам в контейнере?
Рекомендуется ограничивать доступ контейнеров к ресурсам хоста:
1. **Запуск контейнера без root-привилегий**

docker run -d --user 1000:1000 nginx

2. **Ограничение использования CPU и RAM**

docker run -d --memory=512m --cpus="1.0" nginx

Как сканировать контейнер на уязвимости?
Для проверки безопасности контейнеров можно использовать `docker scan`.

docker scan my-image

Альтернативные инструменты:
- **Trivy** – сканирует контейнеры на уязвимости.
- **Clair** – анализирует слои образов Docker.
- **Anchore** – проводит полную проверку безопасности.
Безопасность Docker-контейнеров играет ключевую роль в защите инфраструктуры. Следующим шагом можно рассмотреть оптимизацию контейнеров и уменьшение их размера.
 
8. Оптимизация и продвинутые техники Docker
Оптимизация контейнеров позволяет уменьшить размер образов, ускорить развертывание и улучшить производительность. В этом разделе рассмотрим ключевые техники оптимизации.
Как уменьшить размер Docker-образа?
Основные методы уменьшения размера образа:
- **Использование Alpine Linux** (`node:18-alpine` вместо `node:18`).
- **Удаление временных файлов после установки зависимостей**.
- **Использование multi-stage builds (см. ниже).
Как использовать multi-stage builds?
Multi-stage builds позволяют сначала создать образ с зависимостями и инструментами, а затем скопировать только необходимые файлы в финальный минимальный образ.
Пример multi-stage build для Node.js:

# Первый этап - сборка
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Второй этап - минимальный образ
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY package.json ./
RUN npm install --only=production
CMD ["node", "dist/main.js"]

Как кэшируются слои в Dockerfile?
Docker использует послойное кеширование, чтобы не пересобирать неизменные части образа. Чтобы использовать кеш эффективно, сначала копируются файлы с зависимостями (`package.json`), а затем весь код проекта.
Оптимизированный `Dockerfile`:

FROM node:18

WORKDIR /app

# Сначала копируем package.json и устанавливаем зависимости
COPY package*.json ./
RUN npm install

# Затем копируем исходный код
COPY . .

CMD ["node", "server.js"]

Оптимизация образов позволяет уменьшить их размер, ускорить развертывание и снизить затраты на хранение. Следующим шагом можно рассмотреть Docker Swarm и Kubernetes.
 
9. Docker Swarm и Kubernetes
Docker Swarm и Kubernetes – два популярных инструмента для оркестрации контейнеров. Они позволяют управлять множеством контейнеров, балансировать нагрузку и обеспечивать отказоустойчивость.
Что такое Docker Swarm и как он работает?
**Docker Swarm** – это встроенный в Docker инструмент для оркестрации контейнеров. Он позволяет управлять кластерами контейнеров и автоматически распределять нагрузку.
Основные команды Docker Swarm:

# Инициализация Swarm-кластера
docker swarm init

# Добавление нового узла (worker)
docker swarm join --token <TOKEN> <MANAGER_IP>:2377

# Просмотр узлов кластера
docker node ls

# Развертывание сервиса в Swarm
docker service create --name web -p 8080:80 nginx

# Масштабирование сервиса (5 экземпляров)
docker service scale web=5

# Остановка Swarm-кластера
docker swarm leave --force

Чем Docker Swarm отличается от Kubernetes?
Основные различия между Docker Swarm и Kubernetes:
- **Docker Swarm** проще в настройке и интеграции с Docker.
- **Kubernetes** обладает более мощными возможностями автоматического масштабирования и отказоустойчивости.
- **Swarm** ориентирован на небольшие кластеры, **Kubernetes** – на сложные микросервисные архитектуры.
Какие основные компоненты в Kubernetes?
Kubernetes состоит из нескольких ключевых компонентов:
- **Pod** – минимальная единица Kubernetes, содержащая один или несколько контейнеров.
- **Node** – физический или виртуальный сервер, на котором работают Pods.
- **Deployment** – контролирует развертывание и обновление приложений.
- **Service** – обеспечивает доступ к Pods внутри кластера.
- **Ingress** – управляет маршрутизацией HTTP-запросов.
Как развернуть контейнер в Kubernetes?
Пример манифеста для развертывания Nginx в Kubernetes:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

Команды для развертывания в Kubernetes:

# Применить манифест и развернуть контейнер
kubectl apply -f deployment.yaml

# Проверить запущенные Pods
kubectl get pods

# Удалить развертывание
kubectl delete -f deployment.yaml

Docker Swarm и Kubernetes – мощные инструменты для управления контейнерами в продакшене. Kubernetes предоставляет больше возможностей, но требует сложной настройки.
 
Git
1. Основы Git
Git — это распределённая система управления версиями. Она позволяет разработчикам отслеживать изменения в коде, работать с несколькими ветками и совместно разрабатывать проекты.
Что такое Git и для чего он используется?
Git — это инструмент для контроля версий, который позволяет:
- Хранить историю изменений кода.
- Возвращаться к предыдущим версиям.
- Работать над разными функциями в отдельных ветках.
- Совместно разрабатывать проекты в команде.
В чем разница между `git init` и `git clone`?
`git init` создаёт новый пустой репозиторий в текущей директории:

git init

`git clone` копирует существующий репозиторий (локальный или удалённый) в новую директорию:

git clone https://github.com/username/repository.git

Как добавить файлы в репозиторий? Чем отличается `git add` от `git commit`?
Добавление файла в индекс (staging area):

git add file.txt

`git add` помещает файл в индекс (подготавливает к коммиту).
`git commit` фиксирует изменения в репозитории:

git commit -m "Add file.txt"

Как посмотреть статус репозитория?
Команда `git status` показывает текущие изменения, которые ещё не закоммичены, а также файлы, не добавленные в индекс:

git status

Как узнать, какие изменения были внесены в файл?
Команда `git diff` показывает изменения в текущих файлах по сравнению с последним коммитом:

git diff file.txt

Основы Git позволяют эффективно управлять изменениями кода и организовать совместную работу в команде. Следующим шагом можно рассмотреть работу с ветками.
 
2. Работа с ветками (branches)
Ветки в Git позволяют работать над разными версиями проекта параллельно. Каждая ветка хранит собственную историю коммитов и может быть объединена с основной веткой.
Как создать новую ветку?
Создание ветки с именем `feature-branch`:

git branch feature-branch

Или одновременно создать и переключиться на новую ветку:

git checkout -b feature-branch

Как переключиться на другую ветку?
Используйте команду `git checkout` для перехода на существующую ветку:

git checkout feature-branch

В новых версиях Git предпочтительнее использовать:

git switch feature-branch

Что такое `git checkout` и как он используется?
Команда `git checkout` используется для переключения между ветками, возврата к предыдущим состояниям коммитов или проверки файлов из определённых коммитов.

git checkout main

В чем разница между `git merge` и `git rebase`?
Основные различия:
- **`git merge`**: сохраняет историю изменений в виде точек слияния, удобно для общего потока работы.
- **`git rebase`**: переписывает историю, что делает её более линейной. Это полезно для поддержки чистой истории.

# Merge
git merge feature-branch

# Rebase
git rebase main

Как удалить ветку локально и на удаленном сервере?
Удаление локальной ветки:

git branch -d feature-branch

Удаление ветки на удалённом сервере:

git push origin --delete feature-branch

Работа с ветками в Git позволяет параллельно разрабатывать новые функции, исправлять ошибки и эффективно управлять версиями проекта. Следующим шагом можно рассмотреть способы сравнения изменений.
 
3. Сравнение и просмотр изменений
Git предоставляет множество инструментов для сравнения изменений между файлами, коммитами и ветками. Это помогает отслеживать прогресс работы и находить ошибки на ранних стадиях.
Как посмотреть разницу между текущими изменениями и последним коммитом?
Используйте `git diff` для сравнения текущих изменений с последним коммитом:

git diff

Как узнать, какие изменения были внесены в ветке перед ее слиянием?
Чтобы увидеть все изменения в ветке перед слиянием, используйте `git log` с указанием базовой ветки:

git log main..feature-branch

Это покажет коммиты, которые есть в `feature-branch`, но отсутствуют в `main`.
Что делает `git diff` и как им пользоваться?
`git diff` позволяет увидеть различия между разными состояниями кода. Например:

# Сравнить текущие изменения с последним коммитом
git diff

# Сравнить два коммита
git diff commit1 commit2

# Сравнить ветки
git diff branch1 branch2

Как посмотреть историю изменений в репозитории?
Команда `git log` отображает историю коммитов:

git log

Дополнительно можно использовать параметры для детального просмотра:

# Вывести историю с графом веток
git log --graph --oneline --all

Чем отличается `git log` от `git reflog`?
`git log` показывает историю коммитов в репозитории, тогда как `git reflog` отслеживает все перемещения HEAD, включая изменения, не зафиксированные в истории.

# Посмотреть историю коммитов
git log

# Посмотреть историю всех перемещений HEAD
git reflog

Сравнение изменений в Git помогает отслеживать прогресс разработки и быстро находить причины ошибок. Следующим шагом можно рассмотреть работу с удалёнными репозиториями.
 
4. Работа с удаленными репозиториями
Удалённые репозитории позволяют работать с Git-проектом на разных устройствах и в команде. Они хранятся на внешнем сервере и позволяют совместно управлять кодом.
Как добавить удаленный репозиторий?
Добавление удалённого репозитория выполняется с помощью команды `git remote add`:

git remote add origin https://github.com/username/repository.git

Здесь `origin` — это имя для удалённого репозитория.
Как получить изменения с удаленного репозитория?
Команда `git fetch` скачивает изменения из удалённого репозитория, но не объединяет их с текущей веткой:

git fetch origin

Чтобы получить изменения и сразу их объединить, используйте:

git pull origin main

Что делает `git fetch` и чем он отличается от `git pull`?
Основные различия:
- `git fetch` только скачивает изменения, не затрагивая рабочую ветку.
- `git pull` скачивает изменения и сразу пытается объединить их с текущей веткой.
Как отправить изменения в удаленный репозиторий?
После выполнения коммитов изменения отправляются с помощью команды `git push`:

git push origin main

Как работать с несколькими удаленными репозиториями?
Вы можете добавить несколько удалённых репозиториев и переключаться между ними. Например:

# Добавить второй удалённый репозиторий
git remote add upstream https://github.com/anotheruser/repository.git

# Скачивать изменения с основного репозитория
git fetch upstream

# Отправлять изменения в свой форк
git push origin main

Работа с удалёнными репозиториями позволяет организовать командную работу и сохранять изменения в безопасном месте. Следующим шагом можно рассмотреть управление конфликтами и восстановление.
 
5. Управление конфликтами и восстановление
Иногда при слиянии веток или применении изменений в Git могут возникнуть конфликты. Git предоставляет инструменты для их разрешения, а также для восстановления случайно удалённых или изменённых данных.
Как Git обнаруживает конфликты при слиянии?
Git обнаруживает конфликты, если изменения в разных ветках затрагивают одни и те же строки в файлах. В таких случаях Git отмечает конфликтные участки специальными маркерами в файлах.
Как разрешить конфликт и продолжить слияние?
1. Откройте файл с конфликтами.
2. Найдите маркеры конфликтов (например, `<<<<<<< HEAD` и `=======`).
3. Вручную выберите правильные изменения или объедините оба варианта.
4. После разрешения всех конфликтов добавьте изменённые файлы в индекс:

git add conflicted_file.txt

5. Завершите слияние:

git commit

Что такое `git stash` и как его использовать?
`git stash` временно сохраняет незакоммиченные изменения, чтобы переключиться на другую ветку или выполнить другую операцию.

# Сохранить текущие изменения
git stash

# Вернуть сохранённые изменения
git stash apply

# Удалить сохранённый стэш
git stash drop

Как вернуть удаленный файл?
Если файл был удалён, его можно восстановить из последнего коммита:

git checkout HEAD -- file.txt

Если файл был удалён, но ещё не закоммичен, можно отменить удаление:

git restore file.txt

Что делать, если вы случайно закоммитили в мастер, а нужно было в другую ветку?
Используйте `git reset` для отмены последнего коммита в мастер:

# Отменить последний коммит (оставив изменения в рабочей области)
git reset HEAD~1

# Переключиться на нужную ветку
git checkout feature-branch

# Добавить изменения и закоммитить
git add .
git commit -m "Moved changes to feature-branch"

Управление конфликтами и восстановление позволяет эффективно решать проблемы, возникающие в процессе разработки. Следующим шагом можно рассмотреть использование тегов и релизов.
 
6. Теги и релизы
Теги в Git используются для пометки определённых коммитов, таких как версии релизов. Это упрощает отслеживание изменений и помогает быстро находить стабильные версии кода.
Что такое тег (tag) в Git?
Тег в Git — это указатель на определённый коммит. Он не изменяется со временем, в отличие от веток, и чаще всего используется для обозначения релизов.
Как создать аннотированный тег?
Аннотированный тег включает метаинформацию, такую как имя автора и комментарий. Он создаётся командой `git tag -a`.

git tag -a v1.0 -m "Release version 1.0"

После создания тега его можно отправить на удалённый сервер:

git push origin v1.0

Как удалить тег?
Для удаления локального тега используйте:

git tag -d v1.0

Для удаления тега с удалённого репозитория выполните:

git push origin --delete v1.0

Чем тег отличается от ветки?
Основные различия:
- **Ветка** — это указатель, который может перемещаться по мере новых коммитов.
- **Тег** — это фиксированная отметка, указывающая на конкретный коммит.
- Теги обычно используются для обозначения релизов, а ветки — для разработки.
Как использовать теги для подготовки релизов?
Теги позволяют помечать стабильные версии кода, которые затем можно публиковать в качестве релизов.

# Создать аннотированный тег для новой версии
git tag -a v2.0 -m "Release version 2.0"

# Отправить тег на удалённый репозиторий
git push origin v2.0

Таким образом, каждый релиз имеет свой уникальный идентификатор, связанный с определённым коммитом.
Работа с тегами и релизами в Git помогает организовать процесс разработки и публикации версий. Следующим шагом можно рассмотреть продвинутые вопросы, такие как `git cherry-pick` и `git bisect`.
 
7. Продвинутые вопросы
Git предоставляет мощные инструменты для решения сложных задач, таких как выборочные переносы изменений, поиск ошибок в истории, настройка алиасов и работа с подмодулями.
Как работает `git cherry-pick` и зачем он нужен?
`git cherry-pick` позволяет перенести отдельный коммит из одной ветки в другую, не затрагивая остальную историю.

# Выберите коммит и примените его в текущей ветке
git cherry-pick commit_hash

Этот инструмент полезен, если нужно взять одно конкретное исправление из ветки и применить его в другой ветке, не выполняя полное слияние.
Что делает `git bisect` и как им пользоваться?
`git bisect` помогает найти коммит, который ввёл ошибку, путём двоичного поиска по истории.

# Начать bisect
git bisect start

# Указать известный хороший коммит
git bisect good commit_hash

# Указать коммит, в котором обнаружена ошибка
git bisect bad commit_hash

# Следовать указаниям Git для проверки каждого найденного промежуточного коммита
# и отмечать их как good или bad

# После нахождения виновного коммита
git bisect reset

Это сокращает время поиска ошибки, особенно в крупных проектах с длинной историей.
Как настроить алиасы для команд Git?
Git позволяет создавать алиасы для часто используемых команд, чтобы сократить время на их ввод.

# Добавить алиас через git config
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status

# Теперь можно использовать:
git co main
git br
git st

Алиасы упрощают повседневную работу с Git и повышают производительность.
Чем отличается `git reset --hard` от `git reset --soft`?
Основные отличия:
- **`git reset --soft`**: перемещает HEAD на указанный коммит, сохраняя изменения в индексе и рабочей директории.
- **`git reset --hard`**: перемещает HEAD на указанный коммит и полностью удаляет изменения из индекса и рабочей директории.
Как работает `git submodule` и зачем он нужен?
`git submodule` позволяет включить один репозиторий внутрь другого. Это полезно, если ваш проект зависит от другого репозитория, например, библиотеки.

# Добавить подмодуль
git submodule add https://github.com/user/repo.git path/to/submodule

# Обновить подмодули
git submodule update --init --recursive

# Удалить подмодуль
git submodule deinit -f path/to/submodule
rm -rf .git/modules/path/to/submodule
rm -rf path/to/submodule

Использование подмодулей позволяет синхронизировать зависимые проекты и поддерживать их в актуальном состоянии.
Продвинутые команды Git предоставляют мощные инструменты для управления историей, выбора отдельных коммитов, поиска ошибок и упрощения повседневной работы. Они полезны как для индивидуальных разработчиков, так и для команд.
 
RabbitMQ
1. Основы RabbitMQ
RabbitMQ — это брокер сообщений, который используется для обмена данными между различными компонентами системы. Он помогает организовать асинхронное взаимодействие между микросервисами, обработчиками событий и другими элементами архитектуры.
Что такое RabbitMQ и для чего он используется?
RabbitMQ — это программное обеспечение, которое реализует протокол AMQP (Advanced Message Queuing Protocol). Оно используется для отправки, получения и обработки сообщений. RabbitMQ позволяет распределять задачи, снижать связность компонентов и обеспечивать гибкость архитектуры.
Чем отличается RabbitMQ от других брокеров сообщений?
RabbitMQ поддерживает AMQP, который является стандартным протоколом, обеспечивающим надежную доставку сообщений, широкую совместимость и богатый набор функций. Он прост в установке, имеет удобный веб-интерфейс для управления и мониторинга, а также обеспечивает гибкую настройку маршрутизации сообщений.
Какие основные концепции нужно знать, чтобы работать с RabbitMQ?
Ключевые концепции RabbitMQ:
- **Queue (очередь)**: место, где хранятся сообщения до их получения.
- **Exchange (обменник)**: компонент, который направляет сообщения в очереди.
- **Binding (связывание)**: связь между обменником и очередью.
- **Routing key (ключ маршрутизации)**: ключ, который помогает направлять сообщения.
- **Consumer (потребитель)**: приложение или компонент, который получает сообщения из очереди.
Понимание основных концепций RabbitMQ помогает эффективно использовать брокер сообщений для построения асинхронных систем. Следующим шагом можно рассмотреть его основные компоненты.
 
2. Компоненты RabbitMQ
RabbitMQ состоит из нескольких ключевых компонентов, которые работают вместе для маршрутизации, хранения и доставки сообщений.
Что такое очередь (Queue) в RabbitMQ?
Очередь — это хранилище сообщений, в которое отправляются данные, пока потребители не извлекут их. Очередь принимает сообщения от обменника и выдаёт их потребителям. Сообщения в очереди сохраняются до тех пор, пока они не будут подтверждены или удалены.
Что такое обменник (Exchange) и какие бывают типы обменников?
Обменник принимает сообщения от отправителей и распределяет их в очереди в соответствии с установленными правилами.
Существуют следующие типы обменников:
- **Direct**: сообщения направляются в очередь, ключ маршрутизации которой совпадает с ключом сообщения.
- **Fanout**: сообщения отправляются во все связанные очереди, игнорируя ключ маршрутизации.
- **Topic**: сообщения направляются в очереди, ключ маршрутизации которых соответствует шаблону.
- **Headers**: сообщения распределяются на основе содержимого заголовков.
Какой тип обменника вы бы использовали для широковещательной доставки?
Для широковещательной доставки (рассылки сообщения сразу во все очереди) используется обменник типа **Fanout**.
В чем разница между персистентными и не персистентными очередями?
Основные различия:
- **Персистентные очереди** сохраняются на диске, что позволяет восстановить их после перезапуска брокера.
- **Не персистентные очереди** существуют только в памяти и теряются при перезапуске RabbitMQ.
Что такое биндинг (Binding) и как он работает?
Биндинг — это связь между обменником и очередью. Он указывает, какие сообщения из обменника должны попадать в данную очередь. Биндинг может быть основан на ключе маршрутизации или шаблоне.
Понимание компонентов RabbitMQ помогает правильно настраивать маршрутизацию сообщений и организовывать доставку данных. Следующим шагом можно рассмотреть, как отправлять и получать сообщения.

3. Отправка и получение сообщений
Отправка и получение сообщений — ключевая функциональность RabbitMQ. Она позволяет публиковать данные в очереди и обрабатывать их потребителями.
Как отправить сообщение в RabbitMQ? Какой командой это делается?
Сообщение отправляется через обменник в одну или несколько очередей. Для этого используется клиентская библиотека AMQP (например, amqplib для Node.js или pika для Python).

# Пример отправки сообщения в Node.js
channel.publish('exchangeName', 'routingKey', Buffer.from('Hello, RabbitMQ!'));

Как подписаться на очередь и получать сообщения?
Для получения сообщений из очереди необходимо подписаться на неё через канал. Сообщения будут передаваться потребителю по мере их появления.

# Пример получения сообщения в Node.js
channel.consume('queueName', (msg) => {
  console.log('Received:', msg.content.toString());
  channel.ack(msg);
});

Что произойдет, если отправить сообщение без указанной очереди?
Если сообщение отправляется без указанной очереди, оно передаётся только в обменник. Чтобы сообщение достигло конечной точки, необходимо указать маршрут (routing key), по которому обменник перенаправит сообщение в соответствующую очередь.
Чем отличается подтверждение сообщений (ack) от auto-acknowledgement?
Подтверждение сообщений (acknowledgement) используется для уведомления RabbitMQ о том, что сообщение обработано. Если сообщение не подтверждено, оно останется в очереди или будет переотправлено.
Различия:
- **Manual ack**: приложение явно подтверждает сообщение после его обработки.
- **Auto-ack**: RabbitMQ автоматически считает сообщение обработанным, как только оно доставлено.
Что произойдет, если приложение не подтвердит сообщение (ack)?
Если приложение не отправит подтверждение (ack), сообщение останется в очереди. При этом RabbitMQ может попытаться доставить его повторно другому потребителю.
Правильная настройка отправки и получения сообщений позволяет эффективно обрабатывать данные в RabbitMQ. Следующим шагом можно рассмотреть вопросы производительности и масштабируемости.
 
4. Производительность и масштабируемость
RabbitMQ предоставляет гибкие возможности масштабирования и может работать в высоконагруженных средах. Правильная настройка производительности помогает поддерживать стабильную работу системы при увеличении нагрузки.
Как RabbitMQ обеспечивает масштабируемость?
RabbitMQ поддерживает горизонтальное масштабирование через кластеры и виртуальные хосты. Кластеризация позволяет распределять нагрузку между несколькими узлами, а виртуальные хосты помогают разделять логические окружения.
Что такое кластер RabbitMQ и как он работает?
Кластер RabbitMQ — это несколько узлов (серверов), которые работают вместе как единое целое. Кластер позволяет распределять сообщения и очереди между узлами, обеспечивая отказоустойчивость и масштабируемость.

# Пример команды для добавления узла в кластер
rabbitmqctl join_cluster rabbit@othernode

Какие меры можно предпринять для повышения производительности RabbitMQ?
Рекомендации для повышения производительности:
- Использовать персистентность только там, где это необходимо, чтобы снизить нагрузку на диск.
- Настроить политики TTL и ограничение длины очередей.
- Избегать больших очередей: делите сообщения между несколькими очередями.
- Использовать подтверждения сообщений (ack) для предотвращения переполнения памяти.
- Настроить мониторинг и метрики для своевременного выявления проблем.
В чем разница между конфигурацией master-slave и quorum queues?
- **Master-slave**: один узел выступает в качестве мастера, остальные как резервные. При отказе мастера нужно вручную выбрать нового мастера.
- **Quorum queues**: используют распределённый журнал, автоматически выбирают лидера и обеспечивают лучшую отказоустойчивость.
Правильная настройка производительности и масштабируемости RabbitMQ помогает поддерживать надёжную работу системы при высоких нагрузках. Следующим шагом можно рассмотреть вопросы безопасности и авторизации.
 
5. Безопасность и авторизация
RabbitMQ предоставляет встроенные механизмы управления доступом, аутентификации и защиты данных. Это помогает гарантировать, что только авторизованные пользователи могут отправлять и получать сообщения.
Какие механизмы авторизации есть в RabbitMQ?
RabbitMQ поддерживает следующие механизмы авторизации:
- **Локальные пользователи**: пользователи и их пароли хранятся в самом RabbitMQ.
- **LDAP**: интеграция с корпоративными системами аутентификации.
- **Плагины и сторонние системы**: кастомные модули авторизации.
Как настроить пользователей и права доступа в RabbitMQ?
Пример создания пользователя и настройки прав:

# Создать пользователя
rabbitmqctl add_user username password

# Назначить права доступа
rabbitmqctl set_permissions -p / vhost username ".*" ".*" ".*"

# Проверить текущие права
rabbitmqctl list_permissions -p /

Гибкая система разрешений позволяет задать, кто и к каким ресурсам имеет доступ.
Какие протоколы безопасности поддерживает RabbitMQ?
RabbitMQ поддерживает шифрование соединений с помощью TLS. Это позволяет защитить данные во время передачи между клиентами и сервером.

# Пример включения TLS
# В файле конфигурации rabbitmq.conf добавьте:
listeners.ssl.default = 5671
ssl_options.cacertfile = /path/to/ca_certificate.pem
ssl_options.certfile = /path/to/server_certificate.pem
ssl_options.keyfile = /path/to/server_key.pem

Использование TLS обеспечивает шифрование данных и защиту от перехвата.
Механизмы безопасности и авторизации RabbitMQ помогают защитить данные и контролировать доступ к ресурсам. Следующим шагом можно рассмотреть мониторинг и управление RabbitMQ.
 
6. Мониторинг и управление
Эффективный мониторинг и управление RabbitMQ помогают обеспечить стабильность системы и быстро выявлять проблемы. Для этого RabbitMQ предлагает встроенные инструменты и плагины.
Как мониторить RabbitMQ?
Основные подходы к мониторингу:
- Использование RabbitMQ Management Plugin для визуального отслеживания очередей, обменников, подключений.
- Отслеживание метрик с помощью Prometheus и интеграция с Grafana для создания дашбордов.
- Настройка логирования на уровне сервера для выявления ошибок и аномалий.
Какие метрики важны для мониторинга RabbitMQ?
Некоторые ключевые метрики:
- **Количество сообщений в очередях**: помогает оценить, справляются ли потребители с нагрузкой.
- **Скорость поступления и обработки сообщений**: показывает, насколько эффективно обрабатываются данные.
- **Подключения и каналы**: количество активных соединений и каналов.
- **Потребление ресурсов**: использование памяти, процессора и диска.
Что такое RabbitMQ Management Plugin?
RabbitMQ Management Plugin — это встроенный веб-интерфейс для администрирования RabbitMQ. Он позволяет управлять очередями, обменниками, пользователями, а также просматривать метрики и журналы событий.

# Включение RabbitMQ Management Plugin
rabbitmq-plugins enable rabbitmq_management

После включения плагина интерфейс становится доступен по адресу `http://localhost:15672`.
Какие инструменты можно использовать для управления RabbitMQ?
Основные инструменты:
- **rabbitmqctl**: командная утилита для управления RabbitMQ (создание пользователей, проверка статуса, настройки кластеров).
- **RabbitMQ Management Plugin**: веб-интерфейс для удобного администрирования.
- **Прометей (Prometheus)** и **Графана (Grafana)**: мониторинг и визуализация метрик.
- **Заготовки логов**: анализ журналов для поиска ошибок и предупреждений.
Настройка мониторинга и использование инструментов управления позволяют поддерживать RabbitMQ в стабильном состоянии и быстро реагировать на возникающие проблемы. Следующим шагом можно рассмотреть распространенные проблемы и их решения.
 
7. Распространенные проблемы и их решения
При работе с RabbitMQ могут возникать типовые проблемы, такие как переполнение очередей, высокая нагрузка на потребителей или некорректная конфигурация. Рассмотрим, как справляться с этими ситуациями.
Что делать, если очередь переполняется?
Переполнение очереди может привести к увеличению времени обработки сообщений и снижению производительности системы. Возможные решения:
- Установить политики TTL и ограничение длины очередей, чтобы автоматически удалять старые сообщения.
- Добавить больше потребителей для обработки сообщений быстрее.
- Оптимизировать логику обработки, чтобы сократить время обработки каждого сообщения.
Как избежать “зависания” сообщений в очереди?
Сообщения могут “зависать” в очереди, если потребители не подтверждают их обработку. Для предотвращения этого:
- Убедитесь, что потребители отправляют ack после успешной обработки сообщения.
- Настройте dead-letter exchange, чтобы перенаправлять сообщения, которые не удалось обработать в течение определённого времени.
- Следите за потребителями и при необходимости перезапускайте их.
Как справляться с высоконагруженными сценариями?
При высокой нагрузке на RabbitMQ можно:
- Распределить нагрузку между несколькими очередями и потребителями.
- Использовать кластеризацию RabbitMQ для масштабирования системы.
- Настроить горизонтальное масштабирование потребителей.
- Оптимизировать параметры подключения (например, prefetch count) для более равномерной загрузки.
Знание распространённых проблем и способов их устранения позволяет поддерживать стабильность RabbitMQ даже в условиях высокой нагрузки. Следующим шагом можно рассмотреть вопросы интеграции RabbitMQ с различными клиентами и протоколами.

 
ООП
1. Основные принципы ООП
Объектно-ориентированное программирование (ООП) — это парадигма программирования, основанная на концепциях объектов и классов. ООП используется для структурирования программ, улучшения читаемости кода и его повторного использования.
Что такое ООП и какие проблемы оно решает?
ООП позволяет организовать код вокруг объектов, которые представляют сущности реального мира. Это помогает улучшить читаемость, поддержку кода и его переиспользование.
Проблемы, которые решает ООП:
- Избыточность кода (код можно повторно использовать через наследование).
- Сложность сопровождения (инкапсуляция упрощает управление кодом).
- Масштабируемость (разделение программы на независимые классы облегчает расширение системы).
Четыре основных принципа ООП
Основные принципы ООП:
- **Абстракция**: выделение ключевых характеристик объекта, скрытие деталей реализации.
- **Инкапсуляция**: ограничение доступа к внутренним данным объекта.
- **Наследование**: создание новых классов на основе существующих.
- **Полиморфизм**: возможность работать с разными типами объектов через единый интерфейс.
Чем ООП лучше процедурного программирования?
Основные преимущества ООП перед процедурным программированием:
- Улучшенная модульность и переиспользование кода.
- Лучшая организация и структурированность кода.
- Простота тестирования и отладки.
- Возможность моделирования реального мира в коде.
Какие минусы у ООП?
Несмотря на преимущества, ООП имеет и некоторые недостатки:
- Повышенное потребление памяти из-за хранения большого количества объектов.
- Более сложная структура кода по сравнению с процедурным программированием.
- Возможны проблемы с производительностью при неправильном использовании.
ООП — мощная парадигма программирования, позволяющая писать читаемый и поддерживаемый код. Понимание основных принципов ООП помогает разработчикам эффективно проектировать приложения.
 
2. Классы и объекты
Классы и объекты — это основные строительные блоки объектно-ориентированного программирования (ООП). Класс определяет структуру и поведение объекта, а объект является конкретным экземпляром класса.
Что такое класс и объект?
Класс — это шаблон (прототип), который определяет свойства и методы для объектов. Объект — это конкретный экземпляр класса, который содержит реальные значения свойств.

class Car {
  constructor(brand, model) {
    this.brand = brand;
    this.model = model;
  }

  displayInfo() {
    console.log(`Car: ${this.brand} ${this.model}`);
  }
}

// Создание объекта
const myCar = new Car('Toyota', 'Camry');
myCar.displayInfo(); // Выведет "Car: Toyota Camry"

Чем класс отличается от структуры?
Основные различия между классом и структурой:
- **Класс** — это ссылочный тип (объекты передаются по ссылке), структура — это значимый тип (копируется при передаче).
- **Классы** поддерживают наследование, структуры — нет.
- **В классах можно использовать модификаторы доступа** (public, private, protected), в структурах это ограничено.
Как создается объект в ООП?
Объекты создаются с помощью оператора `new`, который вызывает конструктор класса и инициализирует его свойства.

const person = new Person('Alice', 25);

Что такое конструктор и деструктор?
Конструктор — это специальный метод класса, который вызывается при создании объекта и выполняет его инициализацию.

class User {
  constructor(name) {
    this.name = name;
  }
}

Деструктор — это метод, который вызывается перед удалением объекта. В языках, использующих автоматическое управление памятью (например, JavaScript, Python), деструкторы используются редко, но в C++ они играют важную роль.
Классы и объекты позволяют моделировать сущности реального мира в программировании, упрощая организацию и поддержку кода.
 
3. Инкапсуляция
Инкапсуляция — это принцип ООП, который ограничивает доступ к внутренним данным объекта и позволяет управлять ими только через определённые методы. Это помогает защитить данные от некорректного использования и делает код более структурированным.
Что такое инкапсуляция и зачем она нужна?
Инкапсуляция скрывает детали реализации объекта и предоставляет интерфейс для безопасного взаимодействия с ним. Она помогает предотвратить случайное изменение данных и делает код более предсказуемым.
Какие модификаторы доступа бывают?
Основные модификаторы доступа в ООП:
- **public** — доступен везде, можно вызывать из любого места кода.
- **private** — доступен только внутри класса, скрыт от внешнего кода.
- **protected** — доступен внутри класса и его наследников.

class User {
  private password: string;

  constructor(public name: string, password: string) {
    this.password = password;
  }

  public getInfo(): string {
    return `User: ${this.name}`;
  }

  private getPassword(): string {
    return this.password;
  }
}

const user = new User('Alice', 'secret123');
console.log(user.getInfo());  // Доступно
// console.log(user.password); // Ошибка: свойство private

Что такое геттеры и сеттеры?
Геттеры и сеттеры позволяют управлять доступом к приватным свойствам объекта. Они позволяют выполнить дополнительную логику при чтении или изменении значений.

class Account {
  private balance: number = 0;

  get getBalance(): number {
    return this.balance;
  }

  set deposit(amount: number) {
    if (amount > 0) {
      this.balance += amount;
    } else {
      console.log("Amount must be positive!");
    }
  }
}

const myAccount = new Account();
myAccount.deposit = 100;  // Вызов сеттера
console.log(myAccount.getBalance);  // Вызов геттера

Как скрыть данные внутри класса?
В большинстве языков программирования данные можно скрыть с помощью модификаторов `private` или `protected`. В JavaScript и TypeScript можно использовать символ `#` перед свойством.

class Secret {
  #hiddenMessage = "This is a secret";

  reveal() {
    return this.#hiddenMessage;
  }
}

const obj = new Secret();
console.log(obj.reveal());  // Доступ есть
// console.log(obj.#hiddenMessage); // Ошибка

Инкапсуляция помогает контролировать доступ к данным, защищает их от случайного изменения и делает код более безопасным и организованным.
 
4. Наследование
Наследование — это механизм ООП, который позволяет одному классу (дочернему) использовать свойства и методы другого класса (родительского). Это помогает избежать дублирования кода и упрощает поддержку программ.
Что такое наследование?
Наследование позволяет одному классу получать свойства и методы другого класса. Дочерний класс может переопределять методы родительского класса и добавлять новые.

class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} издает звук.`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} лает.`);
  }
}

const myDog = new Dog('Шарик');
myDog.speak(); // "Шарик лает."

Как в ООП организуется многократное наследование?
Некоторые языки, такие как Python, поддерживают множественное наследование (класс может наследоваться сразу от нескольких классов). Однако в большинстве языков, таких как Java, TypeScript, используется наследование от одного родительского класса и применение интерфейсов для достижения гибкости.

// JavaScript и TypeScript не поддерживают множественное наследование,
// но можно использовать композицию или mixin-функции.
function CanFly(Base) {
  return class extends Base {
    fly() {
      console.log(`${this.name} летает!`);
    }
  };
}

class Bird {
  constructor(name) {
    this.name = name;
  }
}

class FlyingBird extends CanFly(Bird) {}

const eagle = new FlyingBird('Орел');
eagle.fly(); // "Орел летает!"

Можно ли в ООП запретить наследование?
В некоторых языках можно запретить наследование классов с помощью специальных ключевых слов:
- В **Java** используется `final class`.
- В **C#** используется `sealed class`.
- В **TypeScript** можно скрыть конструктор, делая его `private`.

// Пример запрета наследования в TypeScript
class Singleton {
  private constructor() {} // Закрытый конструктор

  static getInstance() {
    return new Singleton();
  }
}

// class ExtendedSingleton extends Singleton {} // Ошибка!

Что такое виртуальные методы и переопределение методов?
Виртуальные методы — это методы, которые могут быть переопределены в дочерних классах.
Переопределение (override) позволяет изменять поведение унаследованных методов.

class Parent {
  showMessage() {
    console.log("Сообщение от родительского класса");
  }
}

class Child extends Parent {
  showMessage() {
    console.log("Сообщение от дочернего класса");
  }
}

const obj = new Child();
obj.showMessage(); // "Сообщение от дочернего класса"

Наследование помогает создавать иерархии классов, улучшает повторное использование кода и делает программные системы более организованными.
 
5. Полиморфизм
Полиморфизм — это принцип ООП, который позволяет объектам разных классов иметь одинаковый интерфейс, но разное поведение. Это делает код гибким и позволяет использовать одни и те же методы для разных типов объектов.
Что такое полиморфизм?
Полиморфизм позволяет использовать один и тот же интерфейс для различных реализаций. Это делает код более универсальным и удобным для расширения.

class Animal {
  makeSound() {
    console.log("Животное издает звук");
  }
}

class Dog extends Animal {
  makeSound() {
    console.log("Собака лает");
  }
}

class Cat extends Animal {
  makeSound() {
    console.log("Кот мяукает");
  }
}

const animals = [new Dog(), new Cat()];

animals.forEach(animal => animal.makeSound());
// Выведет:
// "Собака лает"
// "Кот мяукает"

В чем разница между статическим и динамическим полиморфизмом?
Полиморфизм бывает двух видов:
- **Статический полиморфизм (перегрузка методов)** — определяется на этапе компиляции.
- **Динамический полиморфизм (переопределение методов)** — определяется во время выполнения программы.

// Пример статического полиморфизма (перегрузка методов)
class MathOperations {
  static sum(a: number, b: number): number;
  static sum(a: number, b: number, c: number): number;

  static sum(a: number, b: number, c?: number): number {
    return c !== undefined ? a + b + c : a + b;
  }
}

console.log(MathOperations.sum(5, 10)); // 15
console.log(MathOperations.sum(5, 10, 20)); // 35

Как реализуется полиморфизм в JavaScript/TypeScript, Java, Python?
Полиморфизм реализуется через наследование и переопределение методов.
- В **JavaScript/TypeScript** используется прототипное наследование и классы.
- В **Java** полиморфизм достигается через абстрактные классы и интерфейсы.
- В **Python** можно переопределять методы напрямую в дочерних классах.

// Пример полиморфизма в Python
class Animal:
    def make_sound(self):
        pass

class Dog(Animal):
    def make_sound(self):
        return "Собака лает"

class Cat(Animal):
    def make_sound(self):
        return "Кот мяукает"

animals = [Dog(), Cat()]
for animal in animals:
    print(animal.make_sound())

Полиморфизм делает код гибким и удобным для расширения, так как позволяет работать с разными объектами через единый интерфейс.
 
6. Абстракция
Абстракция — это принцип ООП, который позволяет скрыть сложные детали реализации и предоставить только необходимый интерфейс для взаимодействия с объектами. Это помогает упростить код и сделать его более понятным.
Что такое абстрактный класс?
Абстрактный класс — это класс, который определяет общий интерфейс, но не может быть создан напрямую. Он содержит абстрактные методы, которые должны быть реализованы в дочерних классах.

abstract class Animal {
  constructor(public name: string) {}

  abstract makeSound(): void; // Абстрактный метод без реализации

  move(): void {
    console.log(`${this.name} двигается`);
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Собака лает");
  }
}

const dog = new Dog("Шарик");
dog.makeSound(); // "Собака лает"
dog.move(); // "Шарик двигается"

Чем абстрактный класс отличается от интерфейса?
Основные различия между абстрактным классом и интерфейсом:
- **Абстрактный класс** может содержать реализацию методов, а интерфейс — нет.
- **Класс может наследоваться только от одного абстрактного класса, но реализовывать несколько интерфейсов.**
- **Абстрактный класс** используется, когда нужно предоставить базовую реализацию, а **интерфейс** — когда нужно определить контракт.

// Пример интерфейса в TypeScript
interface Animal {
  makeSound(): void;
}

class Dog implements Animal {
  makeSound(): void {
    console.log("Собака лает");
  }
}

const dog = new Dog();
dog.makeSound(); // "Собака лает"

Можно ли создать объект абстрактного класса?
Нет, абстрактный класс не может быть создан напрямую. Его можно использовать только как базовый класс для наследования.

// Ошибка: Нельзя создать объект абстрактного класса
const animal = new Animal(); // TypeScript выдаст ошибку

Абстракция помогает скрывать ненужные детали реализации, предоставляя только важные части интерфейса. Это делает код более удобным для использования и сопровождения.
 
7. Интерфейсы и композиция
Интерфейсы и композиция — два важных концепта ООП, которые помогают строить гибкие и поддерживаемые программные системы.
Что такое интерфейс в ООП?
Интерфейс — это контракт, который определяет набор методов, но не содержит их реализации. Классы, реализующие интерфейс, обязаны предоставить реализацию этих методов.

interface Animal {
  makeSound(): void;
}

class Dog implements Animal {
  makeSound(): void {
    console.log("Собака лает");
  }
}

const myDog = new Dog();
myDog.makeSound(); // "Собака лает"

В чем разница между наследованием и композицией?
Различия между наследованием и композицией:
- **Наследование** создаёт иерархическую зависимость между классами.
- **Композиция** позволяет включать функциональность других классов без наследования.
- Композиция считается более гибким подходом, так как позволяет изменять поведение объектов во время выполнения.

// Пример композиции в TypeScript
class Engine {
  start() {
    console.log("Двигатель запущен");
  }
}

class Car {
  private engine: Engine;

  constructor() {
    this.engine = new Engine();
  }

  drive() {
    this.engine.start();
    console.log("Машина едет");
  }
}

const myCar = new Car();
myCar.drive();
// "Двигатель запущен"
// "Машина едет"

Почему композиция считается более гибким решением, чем наследование?
Композиция позволяет:
- Избежать жёсткой привязки к родительскому классу.
- Легче изменять и переиспользовать код.
- Изменять поведение объектов во время выполнения.
Использование композиции вместо наследования снижает зависимость между классами и упрощает поддержку кода.
Интерфейсы и композиция позволяют создавать более гибкие и масштабируемые программные системы. Следующим шагом можно рассмотреть принципы SOLID.
 
8. SOLID-принципы
SOLID — это пять основных принципов ООП, которые помогают писать более поддерживаемый, расширяемый и гибкий код.
Что такое SOLID?
SOLID — это аббревиатура, включающая пять ключевых принципов объектно-ориентированного проектирования. Следование этим принципам помогает избежать жёсткой привязки между модулями и улучшить читаемость кода.
S — Принцип единственной ответственности (Single Responsibility)
Класс должен иметь только одну ответственность и изменяться только по одной причине.

// Плохой пример (нарушение принципа SRP)
class Report {
  generate() {
    console.log("Генерация отчета");
  }

  saveToFile() {
    console.log("Сохранение в файл");
  }
}

// Хороший пример (разделение обязанностей)
class ReportGenerator {
  generate() {
    console.log("Генерация отчета");
  }
}

class ReportSaver {
  saveToFile() {
    console.log("Сохранение в файл");
  }
}

O — Принцип открытости/закрытости (Open/Closed)
Классы должны быть **открыты для расширения**, но **закрыты для модификации**.

// Нарушение принципа OCP (нужно изменять существующий код)
class Discount {
  calculate(price, type) {
    if (type === "gold") {
      return price * 0.8;
    } else if (type === "silver") {
      return price * 0.9;
    }
    return price;
  }
}

// Хороший пример (новые скидки можно добавлять через наследование)
interface DiscountStrategy {
  calculate(price: number): number;
}

class GoldDiscount implements DiscountStrategy {
  calculate(price: number): number {
    return price * 0.8;
  }
}

class SilverDiscount implements DiscountStrategy {
  calculate(price: number): number {
    return price * 0.9;
  }
}

L — Принцип подстановки Барбары Лисков (Liskov Substitution)
Подклассы должны корректно заменять родительские классы без изменения поведения программы.

// Нарушение принципа LSP (метод move() есть, но не должен быть у рыб)
class Bird {
  fly() {
    console.log("Птица летает");
  }
}

class Penguin extends Bird {
  fly() {
    throw new Error("Пингвин не умеет летать!");
  }
}

// Улучшенный вариант
interface Bird {
  move(): void;
}

class FlyingBird implements Bird {
  move() {
    console.log("Птица летает");
  }
}

class NonFlyingBird implements Bird {
  move() {
    console.log("Птица ходит");
  }
}

I — Принцип разделения интерфейсов (Interface Segregation)
Не следует заставлять классы реализовывать интерфейсы, которые они не используют.

// Плохой пример (не все животные могут летать)
interface Animal {
  eat(): void;
  fly(): void;
}

class Dog implements Animal {
  eat() {
    console.log("Собака ест");
  }

  fly() {
    throw new Error("Собаки не летают!");
  }
}

// Хороший пример (разделение интерфейсов)
interface Eater {
  eat(): void;
}

interface Flyer {
  fly(): void;
}

class Sparrow implements Eater, Flyer {
  eat() {
    console.log("Воробей ест");
  }

  fly() {
    console.log("Воробей летает");
  }
}

class Dog implements Eater {
  eat() {
    console.log("Собака ест");
  }
}

D — Принцип инверсии зависимостей (Dependency Inversion)
Модули верхнего уровня не должны зависеть от модулей нижнего уровня. Оба должны зависеть от абстракций.

// Плохой пример (высокоуровневый модуль зависит от низкоуровневого)
class MySQLDatabase {
  connect() {
    console.log("Подключение к MySQL");
  }
}

class UserService {
  private db: MySQLDatabase;

  constructor() {
    this.db = new MySQLDatabase();
  }
}

// Хороший пример (использование абстракции)
interface Database {
  connect(): void;
}

class MySQLDatabase implements Database {
  connect() {
    console.log("Подключение к MySQL");
  }
}

class UserService {
  private db: Database;

  constructor(db: Database) {
    this.db = db;
  }
}

Следование принципам SOLID помогает писать код, который легко поддерживать, расширять и тестировать.
 
9. Паттерны проектирования
Паттерны проектирования — это проверенные временем решения распространённых проблем в программировании. Они помогают создавать гибкие, масштабируемые и легко поддерживаемые системы.
Что такое паттерны проектирования?
Паттерн проектирования — это шаблон решения определённой проблемы при проектировании ПО. Паттерны разделяют на три основные группы:
- **Порождающие** (создание объектов: Factory Method, Singleton, Builder).
- **Структурные** (организация объектов: Adapter, Decorator, Composite).
- **Поведенческие** (взаимодействие объектов: Observer, Strategy, Command).
Чем отличаются шаблонные методы от стратегии?
Оба паттерна относятся к поведенческим, но имеют разные принципы работы:
- **Шаблонный метод (Template Method)** задаёт основной алгоритм в базовом классе, а подклассы реализуют отдельные шаги.
- **Стратегия (Strategy)** позволяет выбрать конкретную реализацию алгоритма во время выполнения.

// Пример паттерна "Шаблонный метод"
abstract class DataParser {
  parse() {
    this.readData();
    this.processData();
    this.saveData();
  }

  abstract readData(): void;
  abstract processData(): void;

  saveData() {
    console.log("Сохранение данных");
  }
}

class JSONParser extends DataParser {
  readData() {
    console.log("Чтение JSON");
  }

  processData() {
    console.log("Обработка JSON");
  }
}

const parser = new JSONParser();
parser.parse();

Фабричный метод (Factory Method) и Singleton
**Factory Method** используется для создания объектов без привязки к конкретному классу.

// Пример фабричного метода
abstract class Animal {
  abstract makeSound(): void;
}

class Dog extends Animal {
  makeSound() {
    console.log("Собака лает");
  }
}

class AnimalFactory {
  static createAnimal(type: string): Animal {
    if (type === "dog") {
      return new Dog();
    }
    throw new Error("Неизвестный тип животного");
  }
}

const myAnimal = AnimalFactory.createAnimal("dog");
myAnimal.makeSound(); // "Собака лает"

**Singleton** гарантирует, что у класса есть только один экземпляр.

// Пример Singleton в TypeScript
class Singleton {
  private static instance: Singleton;

  private constructor() {}

  static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }
    return Singleton.instance;
  }
}

const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();

console.log(instance1 === instance2); // true

Использование паттернов проектирования помогает создавать гибкие и масштабируемые архитектуры, что особенно важно в крупных проектах.
 
10. Практические вопросы
На собеседованиях по ООП часто задают вопросы, связанные с практическим применением концепций. Рассмотрим несколько распространённых вопросов и их решения.
Как бы вы спроектировали систему классов для интернет-магазина?
Для интернет-магазина можно выделить основные сущности:
- `Product` (Товар) — содержит информацию о товаре.
- `User` (Пользователь) — представляет клиента.
- `Order` (Заказ) — управляет покупкой товаров.
- `Payment` (Оплата) — отвечает за обработку платежей.
- `Cart` (Корзина) — хранит список товаров перед покупкой.

class Product {
  constructor(public name: string, public price: number) {}
}

class Cart {
  private items: Product[] = [];

  addProduct(product: Product) {
    this.items.push(product);
  }

  getTotal(): number {
    return this.items.reduce((sum, item) => sum + item.price, 0);
  }
}

const cart = new Cart();
cart.addProduct(new Product("Ноутбук", 1000));
console.log(cart.getTotal()); // 1000

Как реализовать пул соединений на основе ООП?
Пул соединений — это механизм управления подключениями к базе данных. Для реализации можно использовать паттерн **Singleton** и очередь соединений.

class Connection {
  constructor(public id: number) {}
}

class ConnectionPool {
  private static instance: ConnectionPool;
  private pool: Connection[] = [];
  private maxSize = 5;

  private constructor() {
    for (let i = 0; i < this.maxSize; i++) {
      this.pool.push(new Connection(i));
    }
  }

  static getInstance(): ConnectionPool {
    if (!this.instance) {
      this.instance = new ConnectionPool();
    }
    return this.instance;
  }

  getConnection(): Connection | null {
    return this.pool.pop() || null;
  }

  releaseConnection(conn: Connection) {
    this.pool.push(conn);
  }
}

const pool = ConnectionPool.getInstance();
const conn = pool.getConnection();
console.log(conn?.id); // Например, 4
pool.releaseConnection(conn!);

Какой принцип ООП помогает сделать код гибким и расширяемым?
Принцип **Открытости/Закрытости (Open/Closed Principle, OCP)** из SOLID говорит, что классы должны быть **открыты для расширения, но закрыты для модификации**. Это позволяет добавлять новую функциональность без изменения существующего кода.

// Добавление новой функциональности через интерфейсы
interface PaymentMethod {
  pay(amount: number): void;
}

class CreditCardPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Оплачено ${amount} через кредитную карту`);
  }
}

class PayPalPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Оплачено ${amount} через PayPal`);
  }
}

// Код, который не нужно менять при добавлении новых методов оплаты
class Checkout {
  process(payment: PaymentMethod, amount: number) {
    payment.pay(amount);
  }
}

const checkout = new Checkout();
checkout.process(new CreditCardPayment(), 100); // "Оплачено 100 через кредитную карту"
checkout.process(new PayPalPayment(), 200); // "Оплачено 200 через PayPal"

Практические вопросы помогают проверить знание ООП в реальных сценариях. Важно не только знать теорию, но и уметь применять принципы ООП в разработке.
 
DRY
Основные принципы DRY
DRY (Don't Repeat Yourself) — это принцип программирования, который гласит, что одна и та же логика не должна повторяться в разных частях кода. Вместо этого код должен быть организован таким образом, чтобы использовать переиспользуемые модули, функции или классы.
Что такое DRY и зачем он нужен?
DRY — это принцип, направленный на устранение дублирования кода. Основные преимущества DRY:
- Упрощение поддержки кода (изменения вносятся в одном месте).
- Улучшение читаемости и структуры кода.
- Уменьшение вероятности ошибок при дублировании логики.
Какие преимущества даёт использование DRY?
Принцип DRY помогает:
- Минимизировать количество багов, так как правки нужно делать только в одном месте.
- Улучшить модульность кода, упрощая повторное использование компонентов.
- Сделать код более понятным и удобным для тестирования.

// Плохой пример (нарушение DRY - дублирование логики)
function calculateDiscountPrice(price) {
  return price * 0.9;
}

function calculateFinalPrice(price) {
  return price * 0.9; // Дублирование
}

// Хороший пример (соблюдение DRY - использование общей функции)
function applyDiscount(price, discount = 0.1) {
  return price * (1 - discount);
}

const price1 = applyDiscount(100);
const price2 = applyDiscount(200, 0.2);

Какие проблемы могут возникнуть при нарушении принципа DRY?
Нарушение DRY может привести к следующим проблемам:
- Дублирование логики усложняет поддержку и модификацию кода.
- Высока вероятность ошибок, так как одно и то же изменение нужно вносить в нескольких местах.
- Код становится менее читаемым и сложнее для тестирования.
Применение DRY делает код более читаемым, удобным в поддержке и масштабируемым. Соблюдение этого принципа особенно важно при разработке крупных проектов.
 
Как соблюдать DRY в коде
Соблюдение принципа DRY позволяет минимизировать дублирование кода и упростить его поддержку. Рассмотрим основные способы предотвращения дублирования.
Как можно избежать дублирования кода?
Основные способы избежать дублирования кода:
- Использование функций и методов для повторяющихся операций.
- Выделение общих частей кода в отдельные модули или классы.
- Использование констант вместо дублирования строк и числовых значений.
- Применение наследования и композиции в ООП.
- Использование шаблонных функций и обобщённого программирования.

// Плохой пример (дублирование логики в разных местах)
function logInfo(message) {
  console.log("[INFO]: " + message);
}

function logError(message) {
  console.log("[ERROR]: " + message);
}

// Хороший пример (общая функция)
function logMessage(level, message) {
  console.log(\`[\${level.toUpperCase()}]: \${message}\`);
}

logMessage("info", "Программа запущена");
logMessage("error", "Произошла ошибка");

Какие методы помогают соблюдать DRY?
Принцип DRY можно реализовать через:
- **Функции**: повторяющиеся действия можно вынести в отдельные функции.
- **Модули**: общий код можно структурировать в модули.
- **Наследование**: создание родительских классов позволяет переиспользовать код.
- **Композицию**: вместо наследования можно использовать композицию для гибкости.

// Пример использования модулей для избежания дублирования
export function calculateTax(price) {
  return price * 0.2;
}

// В другом файле импортируем функцию
import { calculateTax } from "./tax.js";

console.log(calculateTax(100)); // 20

Как применение DRY связано с принципами SOLID?
DRY тесно связан с принципами SOLID:
- **Принцип единственной ответственности (SRP)**: класс или метод должен отвечать только за одну задачу.
- **Принцип открытости/закрытости (OCP)**: код должен быть открыт для расширения, но закрыт для модификации.
- **Принцип инверсии зависимостей (DIP)**: разделение зависимостей улучшает переиспользование кода.
Использование DRY в сочетании с SOLID делает код более поддерживаемым, гибким и масштабируемым. Следующим шагом можно рассмотреть примеры нарушения DRY.
 
Примеры нарушения DRY
Нарушение принципа DRY часто приводит к сложностям в поддержке кода, увеличивает вероятность ошибок и усложняет внесение изменений. Рассмотрим примеры неправильного и правильного подхода.
Пример нарушения DRY и его исправление
Плохой пример (дублирование кода при обработке данных):

// Нарушение DRY: одна и та же логика дублируется в разных функциях
function getUserData(user) {
  return {
    id: user.id,
    name: user.name,
    email: user.email.toLowerCase()
  };
}

function formatAdminData(admin) {
  return {
    id: admin.id,
    name: admin.name,
    email: admin.email.toLowerCase()
  };
}

Исправленный вариант (вынесение повторяющейся логики в общую функцию):

// Соблюдение DRY: выделение повторяющегося кода в отдельную функцию
function formatUserData(entity) {
  return {
    id: entity.id,
    name: entity.name,
    email: entity.email.toLowerCase()
  };
}

const user = formatUserData({ id: 1, name: "Alice", email: "ALICE@MAIL.COM" });
const admin = formatUserData({ id: 2, name: "Bob", email: "BOB@MAIL.COM" });

Почему копипаст в коде — это плохо?
Копирование кода без его переиспользования создаёт следующие проблемы:
- Изменения нужно вносить во множество мест вместо одного.
- Легко допустить ошибку, забыв обновить все дублирующиеся части кода.
- Усложняется поддержка и тестирование.
- Код становится менее читаемым и увеличивается его объем.
Можно ли нарушать DRY? В каких случаях это допустимо?
Хотя DRY является важным принципом, бывают случаи, когда его можно нарушать:
- **Если переиспользование кода усложнит его понимание** (слишком универсальные функции могут запутывать).
- **Если дублирование логики улучшает производительность** (например, в критических участках кода, где важна скорость выполнения).
- **Если разная логика пока совпадает, но может измениться в будущем** (например, в начале проекта, когда бизнес-логика ещё не определена).
Следование принципу DRY помогает улучшить качество кода, но важно помнить, что избыточная оптимизация и чрезмерная универсальность могут ухудшить читаемость и поддержку системы.
 
DRY в архитектуре и базах данных
Принцип DRY применяется не только в коде, но и при проектировании архитектуры приложений и баз данных. Его соблюдение помогает уменьшить дублирование логики и данных, улучшая поддержку и масштабируемость.
Как DRY применяется в проектировании архитектуры?
Способы применения DRY в архитектуре:
- **Выделение повторяющегося кода в сервисы** — например, общие функции авторизации можно вынести в отдельный сервис.
- **Использование слоёв абстракции** — бизнес-логика отделяется от уровня представления (MVC, Clean Architecture).
- **Разделение монолита на модули или микросервисы** — позволяет избежать дублирования кода между разными частями системы.
- **Использование централизованных конфигураций** — позволяет избежать дублирования настроек в разных сервисах.
Как нормализация данных в SQL помогает соблюдать DRY?
Нормализация в базах данных помогает устранить дублирование данных, что является аналогом DRY. Основные принципы нормализации:
- **1NF** (Первая нормальная форма) — исключение дублирующихся столбцов.
- **2NF** (Вторая нормальная форма) — удаление дублирующихся данных в отдельных таблицах.
- **3NF** (Третья нормальная форма) — исключение транзитивных зависимостей.

-- Пример дублирования данных (нарушение DRY)
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_name VARCHAR(255),
    customer_email VARCHAR(255)
);

-- Улучшенный вариант (соблюдение DRY, разделение данных)
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(255),
    email VARCHAR(255)
);

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);

Как микросервисы помогают уменьшить дублирование логики?
В монолитных приложениях одна и та же логика часто дублируется в разных модулях. Микросервисная архитектура позволяет выделять повторяющиеся функции в отдельные сервисы, такие как:
- **Сервис аутентификации** — централизованное управление пользователями и токенами.
- **Сервис платежей** — обработка платежей и выставление счетов.
- **Сервис уведомлений** — отправка email и push-уведомлений.

// Пример API микросервиса для аутентификации
app.post("/login", (req, res) => {
    const { username, password } = req.body;
    const token = authService.authenticate(username, password);
    res.json({ token });
});

Применение DRY в архитектуре и базах данных помогает улучшить масштабируемость и снизить дублирование логики. Следующим шагом можно рассмотреть связь DRY с другими принципами разработки.
 
Связь DRY с другими принципами
DRY тесно связан с другими принципами программирования, такими как KISS, SOLID, и влияет на поддержку, тестирование и разработку API.
Как DRY связан с KISS (Keep It Simple, Stupid)?
KISS (Keep It Simple, Stupid) — принцип, который гласит, что код должен быть максимально простым и понятным. DRY и KISS взаимосвязаны, поскольку уменьшение дублирования кода делает его более читаемым и удобным для поддержки.

// Плохой пример (избыточная сложность, нарушение KISS и DRY)
function calculatePriceWithTax(price, taxRate = 0.2) {
  if (taxRate) {
    return price + (price * taxRate);
  } else {
    return price;
  }
}

// Хороший пример (соблюдение DRY и KISS)
function calculatePrice(price, taxRate = 0.2) {
  return price * (1 + taxRate);
}

Как DRY влияет на поддержку и тестирование кода?
Принцип DRY улучшает поддержку и тестирование, поскольку уменьшает количество мест, где требуется обновлять код. Если одна и та же логика вынесена в отдельный метод или модуль, изменения и исправления ошибок вносятся в одном месте.

// Плохой пример (тестирование усложнено из-за дублирования)
function validateEmail(email) {
  return email.includes("@") && email.length > 5;
}

function validateUser(user) {
  return user.email.includes("@") && user.email.length > 5 && user.name.length > 3;
}

// Хороший пример (использование DRY для улучшения тестирования)
function isValidEmail(email) {
  return email.includes("@") && email.length > 5;
}

function validateUser(user) {
  return isValidEmail(user.email) && user.name.length > 3;
}

Как DRY помогает при разработке API и REST-сервисов?
DRY особенно важен при проектировании API и REST-сервисов, так как уменьшает дублирование бизнес-логики. Использование сервисных слоёв, общих middleware и DTO (Data Transfer Objects) помогает устранить дублирование.

// Плохой пример (дублирование логики в разных маршрутах API)
app.post("/register", async (req, res) => {
  const user = new User(req.body);
  user.password = hashPassword(req.body.password);
  await user.save();
  res.status(201).json(user);
});

app.post("/update-profile", async (req, res) => {
  const user = await User.findById(req.body.id);
  user.password = hashPassword(req.body.password); // Дублирование логики хеширования
  await user.save();
  res.status(200).json(user);
});

// Хороший пример (вынесение логики в сервис)
class UserService {
  static async saveUser(data) {
    data.password = hashPassword(data.password);
    return new User(data).save();
  }
}

app.post("/register", async (req, res) => {
  const user = await UserService.saveUser(req.body);
  res.status(201).json(user);
});

app.post("/update-profile", async (req, res) => {
  const user = await UserService.saveUser(req.body);
  res.status(200).json(user);
});

Связь DRY с другими принципами программирования позволяет сделать код более читаемым, тестируемым и удобным для сопровождения. Использование DRY вместе с KISS и SOLID способствует созданию качественной архитектуры.
 
KISS
Основы принципа KISS
KISS (Keep It Simple, Stupid) — это принцип разработки программного обеспечения, который гласит, что код должен быть максимально простым и понятным. Чем сложнее код, тем больше вероятность ошибок, тем труднее его поддерживать и тестировать.
Что такое KISS и зачем он нужен?
KISS — это принцип, который ориентирован на упрощение кода. Его основные преимущества:
- Уменьшение сложности системы.
- Улучшение читаемости кода.
- Упрощение отладки и тестирования.
- Повышение скорости разработки.
Простота кода делает его более понятным как для текущих разработчиков, так и для тех, кто будет поддерживать его в будущем.
Как KISS влияет на читаемость и поддержку кода?
Чем проще код, тем легче его читать и поддерживать. Сложные конструкции, перегруженные классы и функции затрудняют понимание и отладку.

// Плохой пример (нарушение KISS)
function calculateTotal(items) {
  let total = 0;
  for (let i = 0; i < items.length; i++) {
    total += items[i].price * items[i].quantity;
  }
  return total;
}

// Хороший пример (следование KISS)
function calculateTotal(items) {
  return items.reduce((sum, item) => sum + item.price * item.quantity, 0);
}

Как определить, что код слишком сложный и нарушает KISS?
Признаки нарушения KISS:
- Код трудно читать и понимать даже опытному разработчику.
- Функции и классы слишком перегружены логикой.
- Используется слишком много уровней абстракции без необходимости.
- Избыточное использование шаблонов проектирования, усложняющее код.
- Появление повторяющихся фрагментов кода (что также нарушает DRY).
Применение KISS делает код более понятным, легким в сопровождении и масштабировании. Следующим шагом можно рассмотреть его применение в программировании.
 
Применение KISS в программировании
Соблюдение KISS помогает писать код, который легко читать, поддерживать и тестировать. Чем меньше ненужной сложности, тем быстрее и эффективнее разработка.
Какие практики помогают соблюдать KISS?
Основные методы, помогающие соблюдать KISS:
- **Разделение кода на небольшие функции и модули.**
- **Использование понятных названий переменных и функций.**
- **Избегание ненужных абстракций и усложнений.**
- **Использование простых и понятных структур данных.**
- **Минимизация количества зависимостей.**

// Плохой пример (излишне сложная логика в одной функции)
function processOrder(order) {
  let total = 0;
  order.items.forEach(item => {
    let priceWithTax = item.price * 1.2;
    let discount = item.isOnSale ? 0.1 : 0;
    total += priceWithTax * (1 - discount);
  });
  return total;
}

// Хороший пример (разделение логики на функции)
function calculatePriceWithTax(price) {
  return price * 1.2;
}

function applyDiscount(price, isOnSale) {
  return price * (isOnSale ? 0.9 : 1);
}

function calculateOrderTotal(order) {
  return order.items.reduce((sum, item) => sum + applyDiscount(calculatePriceWithTax(item.price), item.isOnSale), 0);
}

Как использование KISS связано с DRY и SOLID?
Принципы DRY, SOLID и KISS взаимосвязаны:
- **DRY (Don’t Repeat Yourself)** помогает избавиться от дублирования кода, что упрощает поддержку.
- **SOLID** (особенно SRP — принцип единственной ответственности) способствует созданию простых классов и методов.
- **KISS** дополняет эти принципы, требуя минимальной сложности в решении задач.
Можно ли переусердствовать с упрощением кода? Когда KISS может навредить?
Иногда чрезмерное упрощение может навредить. Например:
- Если код становится слишком линейным, без учёта будущего расширения.
- Если игнорируются лучшие практики ради краткости.
- Если из-за избыточного упрощения код становится менее гибким и трудно масштабируемым.

// Плохой пример (избыточное упрощение, затрудняющее расширение)
function processPayment(amount, method) {
  if (method === "credit") {
    console.log("Оплата кредитной картой: " + amount);
  } else if (method === "paypal") {
    console.log("Оплата через PayPal: " + amount);
  } else {
    console.log("Неподдерживаемый метод оплаты");
  }
}

// Хороший пример (использование стратегий, но без лишних усложнений)
class PaymentMethod {
  pay(amount) {
    throw "Метод должен быть реализован";
  }
}

class CreditCardPayment extends PaymentMethod {
  pay(amount) {
    console.log("Оплата кредитной картой: " + amount);
  }
}

class PayPalPayment extends PaymentMethod {
  pay(amount) {
    console.log("Оплата через PayPal: " + amount);
  }
}

const payment = new CreditCardPayment();
payment.pay(100);

Принцип KISS делает код понятным и удобным, но его нужно применять разумно, избегая избыточного упрощения, которое может снизить гибкость архитектуры.
 
Примеры нарушения KISS
Нарушение KISS делает код сложным для понимания и поддержки. Рассмотрим примеры сложных решений и их упрощённые версии.
Пример сложного кода и его упрощение
Плохой пример (избыточная сложность):

// Плохой пример (излишняя сложность, трудно читается)
function calculateSalary(employee) {
  let baseSalary = employee.hoursWorked * employee.hourlyRate;
  let tax = 0;
  if (employee.type === "full-time") {
    tax = baseSalary * 0.2;
  } else if (employee.type === "part-time") {
    tax = baseSalary * 0.1;
  } else if (employee.type === "contractor") {
    tax = baseSalary * 0.05;
  }
  return baseSalary - tax;
}

Хороший пример (упрощенный код, следование KISS):

// Хороший пример (разделение логики, читабельность)
function getTaxRate(employeeType) {
  const rates = { "full-time": 0.2, "part-time": 0.1, "contractor": 0.05 };
  return rates[employeeType] || 0;
}

function calculateSalary(employee) {
  const baseSalary = employee.hoursWorked * employee.hourlyRate;
  const tax = baseSalary * getTaxRate(employee.type);
  return baseSalary - tax;
}

Почему слишком абстрактный или универсальный код может нарушать KISS?
Хотя абстракция помогает соблюдать DRY, чрезмерная универсализация может ухудшить читаемость и усложнить поддержку кода. Примеры:
- Избыточное использование обобщённых типов.
- Создание слишком гибких классов, которые трудно использовать без дополнительного изучения.
- Универсальные утилиты, которые делают всё сразу, вместо простых функций.
Как избежать чрезмерной логики в функциях и классах?
Чтобы избежать перегруженных функций и классов, следуйте этим рекомендациям:
- Разделяйте код на небольшие, легко читаемые функции.
- Используйте принцип единственной ответственности (SRP).
- Избегайте избыточных проверок и вложенных условий.
- Старайтесь писать код, который легко понять без комментариев.

// Плохой пример (перегруженная функция)
function processOrder(order) {
  let total = 0;
  for (let item of order.items) {
    let price = item.price * 1.2; // Добавляем налог
    if (item.isOnSale) {
      price *= 0.9; // Применяем скидку
    }
    total += price;
  }
  console.log("Общая сумма заказа:", total);
}

// Хороший пример (разделение логики)
function calculateItemPrice(item) {
  let price = item.price * 1.2;
  return item.isOnSale ? price * 0.9 : price;
}

function calculateOrderTotal(order) {
  return order.items.reduce((sum, item) => sum + calculateItemPrice(item), 0);
}

console.log("Общая сумма заказа:", calculateOrderTotal(order));

Соблюдение KISS помогает избегать сложных, трудно читаемых конструкций, что делает код более понятным и удобным в поддержке.
 
KISS в архитектуре и проектировании
Принцип KISS применяется не только в коде, но и в проектировании программных систем. Чем проще архитектура, тем легче её разрабатывать, поддерживать и масштабировать.
Как KISS применяется в проектировании систем?
Простая архитектура имеет следующие преимущества:
- Легче внедрять новые функции и исправлять ошибки.
- Уменьшается сложность системы и зависимость между модулями.
- Упрощается тестирование и масштабирование.

// Плохой пример (избыточная сложность, перегруженный класс)
class Order {
  constructor(items, customer, payment) {
    this.items = items;
    this.customer = customer;
    this.payment = payment;
  }

  processOrder() {
    console.log("Обработка заказа...");
    this.payment.charge(this.items.reduce((sum, item) => sum + item.price, 0));
    console.log("Заказ завершен.");
  }
}

// Хороший пример (разделение ответственности)
class PaymentService {
  charge(amount) {
    console.log("Оплата на сумму:", amount);
  }
}

class OrderProcessor {
  constructor(paymentService) {
    this.paymentService = paymentService;
  }

  process(items) {
    const total = items.reduce((sum, item) => sum + item.price, 0);
    this.paymentService.charge(total);
    console.log("Заказ обработан.");
  }
}

const orderProcessor = new OrderProcessor(new PaymentService());
orderProcessor.process([{ price: 100 }, { price: 50 }]);

Почему простая архитектура предпочтительнее сложной?
Сложные архитектуры могут создавать проблемы:
- Труднее разобраться новым разработчикам.
- Увеличивается количество точек отказа в системе.
- Код становится сложным для тестирования и изменений.
Простая архитектура:
- Разделяет логику на небольшие модули.
- Использует понятные и минималистичные API.
- Минимизирует количество зависимостей между компонентами.
Как микросервисный подход и модульность помогают соблюдать KISS?
Микросервисная архитектура и модульность помогают разделять сложные системы на отдельные простые части.
Преимущества:
- Каждая служба отвечает за одну функцию (следование SRP).
- Можно разрабатывать и разворачивать компоненты независимо.
- Снижается сложность каждого отдельного модуля.

// Пример простого микросервиса
const express = require("express");
const app = express();

app.get("/status", (req, res) => {
  res.json({ status: "OK" });
});

app.listen(3000, () => console.log("Сервис работает на порту 3000"));

Простая архитектура по принципу KISS делает системы более надёжными, масштабируемыми и удобными для поддержки. Следующим шагом можно рассмотреть связь KISS с другими принципами.
 
Связь KISS с другими принципами
KISS тесно связан с другими принципами программирования, такими как DRY, YAGNI и SOLID. Следование этим принципам вместе позволяет создавать удобный, поддерживаемый и понятный код.
Как KISS связан с DRY и YAGNI?
- **DRY (Don’t Repeat Yourself)**: Устранение дублирования упрощает код и делает его более читаемым.
- **YAGNI (You Ain’t Gonna Need It)**: Код должен содержать только то, что действительно необходимо, без избыточных функций.
KISS требует избегать сложных решений и избыточной гибкости, что соответствует принципам DRY и YAGNI.

// Плохой пример (избыточная функциональность, нарушение YAGNI)
class User {
  constructor(name, age, address, phone, email, isSubscribed) {
    this.name = name;
    this.age = age;
    this.address = address;
    this.phone = phone;
    this.email = email;
    this.isSubscribed = isSubscribed;
  }
}

// Хороший пример (минимально необходимая структура)
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }
}

Как KISS помогает в тестировании и дебаге?
Чем проще код, тем легче его тестировать. KISS помогает:
- Уменьшить количество потенциальных ошибок.
- Упростить написание юнит-тестов.
- Снизить сложность логики, уменьшая вероятность багов.

// Плохой пример (сложная функция, трудно тестировать)
function calculateFinalPrice(price, discount, tax, loyaltyPoints) {
  let finalPrice = price - (price * discount);
  finalPrice += finalPrice * tax;
  if (loyaltyPoints > 100) {
    finalPrice *= 0.9;
  }
  return finalPrice;
}

// Хороший пример (разделение логики, упрощённое тестирование)
function applyDiscount(price, discount) {
  return price - (price * discount);
}

function applyTax(price, tax) {
  return price + (price * tax);
}

function applyLoyaltyDiscount(price, points) {
  return points > 100 ? price * 0.9 : price;
}

function calculateFinalPrice(price, discount, tax, points) {
  return applyLoyaltyDiscount(applyTax(applyDiscount(price, discount), tax), points);
}

Почему принцип KISS важен для командной разработки?
В командной разработке KISS помогает избежать сложных, трудночитаемых решений, которые затрудняют понимание кода другими разработчиками.
Преимущества KISS в команде:
- Код становится понятным для всех участников проекта.
- Проще вносить изменения и исправлять баги.
- Улучшается совместная работа над проектом.
Применение KISS в сочетании с другими принципами (DRY, YAGNI, SOLID) делает код более читаемым, тестируемым и удобным в сопровождении. Следование этим принципам способствует повышению эффективности разработки.
 
PostgreSQL
Основы PostgreSQL
PostgreSQL — это мощная, объектно-реляционная база данных с открытым исходным кодом. Она поддерживает расширенные функции, такие как MVCC (Multi-Version Concurrency Control), работа с JSONB, полнотекстовый поиск и репликацию.
Что такое PostgreSQL и в чем его особенности?
PostgreSQL — это свободная объектно-реляционная система управления базами данных (ORDBMS), которая отличается высокой надёжностью, расширяемостью и соответствием стандарту SQL.
Основные особенности PostgreSQL:
- Поддержка ACID-транзакций.
- Расширенная работа с JSON и JSONB.
- Мощная система индексов (B-Tree, GIN, GiST, BRIN).
- Поддержка репликации и масштабирования.
- Гибкая система аутентификации и прав доступа.
- Возможность создания пользовательских функций на PL/pgSQL, Python, JavaScript и других языках.
Чем PostgreSQL лучше/хуже MySQL, Oracle, MS SQL?
Сравнение PostgreSQL с другими популярными СУБД:
- **PostgreSQL vs MySQL**: PostgreSQL более гибкий, поддерживает сложные типы данных, но MySQL проще в администрировании и быстрее при простых операциях.
- **PostgreSQL vs Oracle**: PostgreSQL бесплатный, в то время как Oracle — коммерческое решение. PostgreSQL менее ресурсоёмкий, но уступает Oracle в корпоративных возможностях.
- **PostgreSQL vs MS SQL Server**: MS SQL тесно интегрирован с экосистемой Microsoft, но PostgreSQL более кроссплатформенный и имеет более гибкую систему расширений.
Какие основные архитектурные особенности PostgreSQL?
PostgreSQL использует многопроцессную архитектуру, а не многопоточный подход. Это означает, что каждый новый клиент создаёт отдельный процесс на сервере.
Ключевые особенности архитектуры:
- **MVCC (Multi-Version Concurrency Control)**: Позволяет выполнять транзакции без блокировки чтения.
- **WAL (Write-Ahead Logging)**: Журналирование изменений перед их применением в базу данных.
- **Автовакуум**: Поддерживает производительность базы данных, удаляя неиспользуемые строки.
- **Расширяемость**: Возможность добавлять новые типы данных, операторы и функции.
Что такое MVCC (Multi-Version Concurrency Control) и как оно работает?
MVCC (Многоверсионное управление конкурентным доступом) позволяет выполнять параллельные транзакции без блокировки чтения и записи.
Каждая транзакция видит **снимок данных**, а не изменяет данные напрямую. Это уменьшает конфликты между транзакциями и повышает производительность.

-- Проверка уровней изоляции в PostgreSQL
SHOW TRANSACTION ISOLATION LEVEL;

-- Пример транзакции с уровнем SERIALIZABLE
BEGIN;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
SELECT * FROM accounts WHERE id = 1;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
COMMIT;

Какие типы данных поддерживает PostgreSQL?
PostgreSQL поддерживает широкий спектр типов данных, включая:
- **Числовые**: INTEGER, BIGINT, NUMERIC, REAL, DOUBLE PRECISION.
- **Символьные**: CHAR, VARCHAR, TEXT.
- **Дата и время**: DATE, TIME, TIMESTAMP, INTERVAL.
- **Булевы**: BOOLEAN.
- **Массивы**: INTEGER[], TEXT[].
- **JSON и JSONB**: JSON, JSONB (оптимизированный для индексации JSON).
- **Геометрические**: POINT, LINE, CIRCLE, POLYGON.
- **UUID, CIDR, MACADDR, XML**.

-- Создание таблицы с разными типами данных
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email TEXT UNIQUE NOT NULL,
    age INTEGER CHECK (age >= 18),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT NOW()
);

Что такое схема в PostgreSQL и зачем она нужна?
Схема в PostgreSQL — это логическая структура, содержащая таблицы, представления, функции и другие объекты базы данных. Схемы позволяют организовать данные и управлять доступом.

-- Создание новой схемы
CREATE SCHEMA sales;

-- Создание таблицы в конкретной схеме
CREATE TABLE sales.customers (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL
);

-- Доступ к таблице через схему
SELECT * FROM sales.customers;

Понимание основ PostgreSQL помогает эффективно работать с базами данных, настраивать производительность и разрабатывать масштабируемые приложения.
 
Работа с данными в PostgreSQL
PostgreSQL предоставляет мощные инструменты для работы с данными. Можно легко создавать, изменять и удалять данные, а также управлять их целостностью и эффективностью.
Как создать, изменить и удалить таблицу в PostgreSQL?
Создание таблицы:

CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    position TEXT,
    salary NUMERIC(10,2),
    hired_at TIMESTAMP DEFAULT NOW()
);

Изменение таблицы:

ALTER TABLE employees ADD COLUMN department TEXT;
ALTER TABLE employees ALTER COLUMN salary SET NOT NULL;
ALTER TABLE employees DROP COLUMN position;

Удаление таблицы:

DROP TABLE employees;

Какие бывают индексы и как они работают?
PostgreSQL поддерживает различные типы индексов для ускорения поиска данных:
- **B-Tree**: стандартный индекс для быстрого поиска по равенству и диапазонам.
- **Hash**: быстрый поиск по равенству (но менее гибкий, чем B-Tree).
- **GIN (Generalized Inverted Index)**: используется для поиска в `JSONB`, массивов и `FULL TEXT SEARCH`.
- **GiST (Generalized Search Tree)**: применяется для геометрических данных и полнотекстового поиска.
- **BRIN (Block Range INdex)**: оптимизирован для больших таблиц с упорядоченными данными.

-- Создание B-Tree индекса
CREATE INDEX idx_employees_name ON employees(name);

-- Создание GIN индекса для JSONB
CREATE INDEX idx_employees_data ON employees USING GIN (data);

Как работают транзакции и уровни изоляции?
Транзакции позволяют выполнять несколько SQL-операций как единое целое. PostgreSQL поддерживает следующие уровни изоляции транзакций:
- **READ COMMITTED** (по умолчанию): транзакция видит только зафиксированные изменения.
- **REPEATABLE READ**: транзакция видит только данные на момент её начала.
- **SERIALIZABLE**: максимальный уровень изоляции, предотвращает параллельные изменения.

BEGIN;
UPDATE employees SET salary = salary * 1.1 WHERE department = 'IT';
COMMIT;

Что такое `ON CONFLICT` и чем он полезен?
`ON CONFLICT` позволяет обрабатывать дублирующиеся записи без возникновения ошибки `unique_violation`. Можно либо обновлять существующие записи (`DO UPDATE`), либо пропускать (`DO NOTHING`).

INSERT INTO employees (name, department, salary)
VALUES ('John Doe', 'IT', 5000)
ON CONFLICT (name) DO UPDATE SET salary = EXCLUDED.salary;

Работа с данными в PostgreSQL включает создание таблиц, управление индексами и транзакциями, а также обработку конфликтов при вставке. Это помогает эффективно управлять базой данных.
 
Запросы и их оптимизация в PostgreSQL
PostgreSQL предоставляет мощные инструменты для оптимизации запросов, позволяя ускорять выполнение операций и анализировать их эффективность.
Чем отличается `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`?
Основные виды соединений таблиц в PostgreSQL:
- **INNER JOIN** – возвращает только совпадающие записи из обеих таблиц.
- **LEFT JOIN** – возвращает все записи из левой таблицы, а из правой только совпадающие.
- **RIGHT JOIN** – возвращает все записи из правой таблицы, а из левой только совпадающие.
- **FULL JOIN** – возвращает все записи из обеих таблиц, заполняя отсутствующие значения `NULL`.

-- INNER JOIN: выводит только совпадающие записи
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;

-- LEFT JOIN: выводит всех сотрудников, даже если у них нет отдела
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id;

-- RIGHT JOIN: выводит все отделы, даже если в них нет сотрудников
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.id;

-- FULL JOIN: объединяет обе таблицы, заполняя NULL там, где нет совпадений
SELECT employees.name, departments.department_name
FROM employees
FULL JOIN departments ON employees.department_id = departments.id;

Как работает `EXPLAIN ANALYZE` и зачем он нужен?
`EXPLAIN ANALYZE` позволяет анализировать производительность SQL-запросов, показывая, как PostgreSQL выполняет их шаг за шагом.

EXPLAIN ANALYZE SELECT * FROM employees WHERE department_id = 5;

Вывод команды `EXPLAIN ANALYZE` включает информацию о планах выполнения, например, использование индексов (`Index Scan`), последовательного поиска (`Seq Scan`) и сортировки (`Sort`).
Как оптимизировать медленный запрос?
Методы оптимизации запросов в PostgreSQL:
- Использование индексов (`CREATE INDEX`).
- Минимизация использования `SELECT *` (выбирать только нужные столбцы).
- Применение `EXPLAIN ANALYZE` для анализа запросов.
- Избегание сложных `JOIN`, если можно переписать запрос более эффективно.
- Использование **CTE (`WITH`)** для оптимизации сложных запросов.

-- Создание индекса для ускорения выборки по department_id
CREATE INDEX idx_employees_department ON employees(department_id);

-- Использование CTE для улучшения читаемости и производительности запроса
WITH EmployeeCount AS (
    SELECT department_id, COUNT(*) AS employee_count
    FROM employees
    GROUP BY department_id
)
SELECT d.department_name, e.employee_count
FROM departments d
LEFT JOIN EmployeeCount e ON d.id = e.department_id;

Что такое CTE (`WITH`), когда его использовать?
CTE (Common Table Expression) – это временная подзапросная таблица, которая помогает упростить и оптимизировать сложные SQL-запросы.

WITH HighSalaryEmployees AS (
    SELECT name, salary FROM employees WHERE salary > 5000
)
SELECT * FROM HighSalaryEmployees;

CTE полезны, когда:
- Нужно переиспользовать один и тот же подзапрос несколько раз.
- Улучшение читаемости кода делает SQL-запросы более понятными.
- Требуется разложить сложный запрос на более простые шаги.
Оптимизация запросов в PostgreSQL – ключ к высокой производительности. Использование индексов, `EXPLAIN ANALYZE`, CTE и продуманных `JOIN` помогает ускорить выполнение запросов.
 
Расширенные возможности PostgreSQL
PostgreSQL предлагает множество продвинутых функций, таких как хранимые процедуры, работа с JSON, материализованные представления и триггеры. Эти возможности помогают строить мощные и гибкие базы данных.
Что такое хранимые процедуры и триггеры в PostgreSQL?
Хранимые процедуры позволяют выполнять сложную логику внутри базы данных, а триггеры автоматически реагируют на изменения данных в таблицах.

-- Пример хранимой процедуры
CREATE OR REPLACE FUNCTION increase_salary(emp_id INT, percent NUMERIC)
RETURNS VOID AS $$
BEGIN
  UPDATE employees SET salary = salary * (1 + percent / 100) WHERE id = emp_id;
END;
$$ LANGUAGE plpgsql;

-- Вызов процедуры
SELECT increase_salary(1, 10);


-- Пример триггера, который записывает изменения в таблицу логов
CREATE TABLE employee_changes (
    change_id SERIAL PRIMARY KEY,
    emp_id INT,
    change_time TIMESTAMP DEFAULT NOW(),
    action TEXT
);

CREATE OR REPLACE FUNCTION log_employee_changes() RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO employee_changes (emp_id, action) VALUES (NEW.id, 'Updated');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER employee_update_trigger
AFTER UPDATE ON employees
FOR EACH ROW EXECUTE FUNCTION log_employee_changes();

Как работает JSONB и чем он лучше JSON?
PostgreSQL поддерживает два типа хранения JSON-данных: `JSON` (текстовый формат) и `JSONB` (бинарный). `JSONB` лучше, так как позволяет индексировать данные и ускоряет поиск.

-- Создание таблицы с JSONB
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name TEXT,
    attributes JSONB
);

-- Вставка данных
INSERT INTO products (name, attributes) VALUES ('Phone', '{"brand": "Apple", "model": "iPhone 13"}');

-- Поиск по JSONB
SELECT * FROM products WHERE attributes @> '{"brand": "Apple"}';

Что такое материализованные представления (`MATERIALIZED VIEW`)?
Материализованные представления хранят результаты запроса в виде физической таблицы, что ускоряет повторные запросы.

-- Создание материализованного представления
CREATE MATERIALIZED VIEW top_salaries AS
SELECT name, salary FROM employees ORDER BY salary DESC LIMIT 10;

-- Обновление данных в материализованном представлении
REFRESH MATERIALIZED VIEW top_salaries;

Как настроить репликацию и бэкап?
Основные способы бэкапа и репликации PostgreSQL:
- **pg_dump** – создание дампа базы данных.
- **pg_basebackup** – копирование базы для создания реплики.
- **WAL (Write-Ahead Logging)** – механизмы журналирования изменений.
- **Streaming Replication** – потоковая репликация данных между серверами.

-- Создание резервной копии базы данных
pg_dump -U postgres -F c -b -v -f "backup.dump" my_database

-- Восстановление базы данных из дампа
pg_restore -U postgres -d my_database "backup.dump"

Расширенные функции PostgreSQL позволяют работать с JSON, оптимизировать работу с данными и управлять репликацией и бэкапами для высокой доступности.
 
Администрирование и безопасность PostgreSQL
PostgreSQL предоставляет гибкие механизмы управления пользователями, настройки безопасности и мониторинга производительности.
Как создать и управлять пользователями и ролями?
PostgreSQL использует роли вместо традиционных пользователей. Роль может быть пользователем (логин) или группой.

-- Создание пользователя с паролем
CREATE ROLE myuser WITH LOGIN PASSWORD 'securepassword';

-- Создание группы и добавление пользователя в неё
CREATE ROLE admins;
GRANT admins TO myuser;

-- Изменение прав роли
ALTER ROLE myuser CREATEDB;

Как настроить права доступа (`GRANT` и `REVOKE`)?
PostgreSQL позволяет детально настраивать доступ к данным:

-- Разрешить пользователю myuser доступ к таблице employees
GRANT SELECT, INSERT ON employees TO myuser;

-- Запретить пользователю изменять данные
REVOKE UPDATE, DELETE ON employees FROM myuser;

Как мониторить производительность PostgreSQL?
Основные инструменты для мониторинга:
- **pg_stat_activity** – просмотр активных процессов.
- **pg_stat_user_tables** – статистика по таблицам.
- **EXPLAIN ANALYZE** – анализ производительности запросов.
- **pg_stat_bgwriter** – отслеживание работы бэкенд-процессов.

-- Проверка активных подключений
SELECT * FROM pg_stat_activity;

-- Статистика использования таблиц
SELECT relname, seq_scan, idx_scan FROM pg_stat_user_tables;

Что делать, если база данных перегружена?
Основные причины перегрузки PostgreSQL и их решения:
- **Частые full table scan** – добавить индексы.
- **Много заблокированных транзакций** – проверить `pg_stat_activity`.
- **Отсутствие вакуума** – выполнить `VACUUM ANALYZE`.
- **Перегрузка соединений** – ограничить `max_connections` и использовать пул соединений.

-- Освободить заблокированные соединения
SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE state = 'idle';

Администрирование и безопасность PostgreSQL – ключевые аспекты эффективной работы с базой данных. Грамотное управление пользователями, мониторинг и оптимизация помогают поддерживать высокую производительность.
 
Работа с масштабируемостью PostgreSQL
PostgreSQL поддерживает различные методы масштабирования, включая шардирование, партиционирование и распределённые базы данных.
Как PostgreSQL работает с шардированием?
Шардирование позволяет распределять данные по нескольким серверам для повышения производительности и отказоустойчивости.

-- Пример Foreign Data Wrapper (FDW) для шардирования
CREATE EXTENSION postgres_fdw;

-- Создание удалённого сервера
CREATE SERVER shard1 FOREIGN DATA WRAPPER postgres_fdw OPTIONS (host '192.168.1.100', dbname 'shard1_db');

-- Создание пользователя для соединения с удалённым сервером
CREATE USER MAPPING FOR current_user SERVER shard1 OPTIONS (user 'postgres', password 'password');

-- Создание таблицы, ссылающейся на удалённые данные
CREATE FOREIGN TABLE orders_shard1 (
    order_id INT,
    customer_id INT,
    amount NUMERIC
) SERVER shard1 OPTIONS (schema_name 'public', table_name 'orders');

Что такое Foreign Data Wrapper (FDW) и когда его применять?
FDW (Foreign Data Wrapper) позволяет PostgreSQL взаимодействовать с внешними источниками данных, например, другими базами PostgreSQL, MySQL, CSV-файлами и REST API.

-- Подключение к MySQL через FDW
CREATE EXTENSION mysql_fdw;

-- Создание сервера для подключения к MySQL
CREATE SERVER mysql_server FOREIGN DATA WRAPPER mysql_fdw OPTIONS (host 'mysql_host', port '3306');

-- Создание маппинга пользователей
CREATE USER MAPPING FOR current_user SERVER mysql_server OPTIONS (username 'mysql_user', password 'mysql_password');

-- Создание внешней таблицы
CREATE FOREIGN TABLE mysql_customers (
    id INT,
    name TEXT,
    email TEXT
) SERVER mysql_server OPTIONS (dbname 'mydb', table_name 'customers');

Как работает pg_partman (партиционирование данных)?
Партиционирование данных позволяет разделять таблицу на более мелкие части для повышения производительности запросов и упрощения управления данными.

-- Установка расширения pg_partman
CREATE EXTENSION pg_partman;

-- Создание партиционированной таблицы
SELECT partman.create_parent('public.sales', 'sale_date', 'monthly', p_start_partition := '2023-01-01');

-- Вставка данных автоматически распределяется по партициям
INSERT INTO sales (id, sale_date, amount) VALUES (1, '2023-05-15', 200);

В чем разница между партиционированием и таблицами-наследниками?
Партиционирование и наследование позволяют организовывать данные, но отличаются принципами работы.
- **Партиционирование** автоматически распределяет записи по партициям на основе заданного столбца.
- **Наследование** позволяет вручную создавать дочерние таблицы и управлять их связями.

-- Пример наследуемых таблиц
CREATE TABLE parent_table (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE child_table (
    extra_info TEXT
) INHERITS (parent_table);

-- Вставка в родительскую таблицу не добавляет данные в дочернюю
INSERT INTO parent_table (name) VALUES ('Example');

Как эффективно работать с очень большими таблицами?
Методы оптимизации работы с большими таблицами:
- **Использование индексов (B-Tree, GIN, BRIN) для ускорения поиска.**
- **Партиционирование данных для снижения нагрузки на диск.**
- **Автоматическая очистка базы с помощью `VACUUM` и `ANALYZE`.**
- **Использование `EXPLAIN ANALYZE` для диагностики медленных запросов.**

-- Очистка базы данных для оптимизации
VACUUM ANALYZE;

Масштабируемость PostgreSQL достигается через шардирование, партиционирование и оптимизацию работы с большими объёмами данных. Это позволяет эффективно обрабатывать большие нагрузки.
 
Безопасность и защита данных в PostgreSQL
PostgreSQL предлагает мощные инструменты для обеспечения безопасности базы данных, включая управление пользователями, шифрование и защиту от атак.
Как PostgreSQL реализует SSL и шифрование данных?
PostgreSQL поддерживает SSL для защиты передаваемых данных.

# Включение SSL в postgresql.conf
ssl = on
ssl_cert_file = '/etc/postgresql/server.crt'
ssl_key_file = '/etc/postgresql/server.key'

# Подключение с использованием SSL
psql "sslmode=require dbname=mydb user=myuser"

Какие механизмы защиты от SQL-инъекций существуют?
Основные методы защиты от SQL-инъекций:
- **Использование подготовленных выражений (`PREPARE` и `EXECUTE`).**
- **Использование ORM, который предотвращает инъекции.**
- **Проверка входных данных и ограничение прав пользователей.**

-- Использование подготовленных выражений
PREPARE safe_query (TEXT) AS SELECT * FROM users WHERE username = $1;
EXECUTE safe_query('admin');

Как настроить ротацию логов в PostgreSQL?
Ротация логов помогает управлять объемом лог-файлов и предотвращает их переполнение.

# Настройки ротации логов в postgresql.conf
logging_collector = on
log_rotation_age = 1d  # Ротация раз в сутки
log_rotation_size = 100MB  # Лимит размера логов

Как работает RLS (Row-Level Security)?
RLS (Row-Level Security) позволяет ограничивать доступ к данным на уровне строк таблицы, что повышает безопасность.

-- Включение RLS на таблице
ALTER TABLE employees ENABLE ROW LEVEL SECURITY;

-- Создание политики доступа
CREATE POLICY employee_access ON employees
FOR SELECT USING (current_user = manager);

Как PostgreSQL справляется с DDoS-атаками на уровне базы данных?
Методы защиты от DDoS-атак:
- **Ограничение максимального числа подключений (`max_connections`).**
- **Использование connection pool (PgBouncer).**
- **Настройка лимитов запросов через `pg_stat_statements`.**

# Ограничение подключений в postgresql.conf
max_connections = 100

# Настройка лимитов запросов
CREATE EXTENSION pg_stat_statements;
SELECT * FROM pg_stat_statements ORDER BY total_exec_time DESC;

Безопасность PostgreSQL включает защиту данных с помощью SSL, предотвращение SQL-инъекций, управление доступом через RLS и защиту от атак.
 
Индексы и производительность в PostgreSQL
Индексы в PostgreSQL помогают ускорять поиск данных и повышать производительность запросов. Однако неправильное использование индексов может привести к снижению эффективности работы базы данных.
Какие бывают индексы в PostgreSQL?
Основные типы индексов в PostgreSQL:
- **B-Tree** – стандартный индекс для большинства запросов (равенство и диапазоны).
- **Hash** – быстрый поиск по точному совпадению (используется реже).
- **GIN (Generalized Inverted Index)** – индекс для JSONB, массивов и Full-Text Search.
- **GiST (Generalized Search Tree)** – индекс для геометрических и полнотекстовых данных.
- **BRIN (Block Range INdex)** – индекс для больших упорядоченных таблиц.

-- Создание B-Tree индекса
CREATE INDEX idx_employees_name ON employees(name);

-- Создание GIN индекса для JSONB
CREATE INDEX idx_products_attributes ON products USING GIN (attributes);

-- Создание BRIN индекса для больших таблиц
CREATE INDEX idx_large_table_date ON large_table USING BRIN (created_at);

Когда индексы улучшают, а когда ухудшают производительность?
Индексы улучшают производительность, когда:
- Запросы часто выполняются с `WHERE`, `ORDER BY` или `JOIN` по индексируемым полям.
- Таблица содержит большое количество данных, и поиск без индекса был бы медленным.
- Используются сложные типы данных, такие как `JSONB`, массивы или геометрические объекты.
Индексы могут ухудшать производительность, если:
- Таблица маленькая, и индексация даёт лишнюю нагрузку.
- Запросы часто изменяют данные (`INSERT`, `UPDATE`, `DELETE`), так как индексы требуют обновления.
- Индекс создаётся на редко используемое поле, что увеличивает размер базы без выгоды.
Как узнать, какие индексы используются в PostgreSQL?
PostgreSQL предоставляет несколько команд для анализа индексов:

-- Просмотр всех индексов в базе данных
SELECT * FROM pg_indexes WHERE schemaname = 'public';

-- Проверка использования индексов
SELECT relname, idx_scan, idx_tup_read, idx_tup_fetch FROM pg_stat_user_indexes;

-- Анализ плана выполнения запроса
EXPLAIN ANALYZE SELECT * FROM employees WHERE name = 'John';

Как эффективно использовать индексы для оптимизации запросов?
Рекомендации по эффективному использованию индексов:
- Используйте `EXPLAIN ANALYZE` для оценки эффективности запроса.
- Удаляйте неиспользуемые индексы (`DROP INDEX`).
- Используйте составные индексы, если запросы часто фильтруют по нескольким полям.
- Следите за балансом между производительностью чтения и обновления данных.

-- Создание составного индекса
CREATE INDEX idx_orders_customer_date ON orders(customer_id, created_at);

-- Удаление ненужного индекса
DROP INDEX idx_old_unused_index;

Индексы – это мощный инструмент повышения производительности PostgreSQL, но их неправильное использование может негативно сказаться на эффективности работы базы данных.
 
Транзакции и блокировки в PostgreSQL
Транзакции обеспечивают целостность данных в PostgreSQL, а механизмы блокировок позволяют управлять конкурентным доступом к таблицам и строкам.
Как работают транзакции в PostgreSQL?
Транзакция – это группа SQL-операций, выполняемых как единое целое. Если одна из операций не удалась, все изменения откатываются (`ROLLBACK`).

-- Начало транзакции
BEGIN;

-- Выполнение нескольких операций
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- Завершение транзакции
COMMIT;

-- Откат транзакции в случае ошибки
ROLLBACK;

Какие уровни изоляции транзакций поддерживает PostgreSQL?
PostgreSQL поддерживает четыре уровня изоляции транзакций:
- **READ UNCOMMITTED** – транзакция может видеть незавершенные изменения других транзакций.
- **READ COMMITTED** (по умолчанию) – транзакция видит только зафиксированные изменения.
- **REPEATABLE READ** – транзакция фиксирует снимок данных на момент начала и видит только его.
- **SERIALIZABLE** – максимальный уровень изоляции, эмулирует последовательное выполнение транзакций.

-- Установка уровня изоляции перед началом транзакции
BEGIN;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
SELECT * FROM accounts WHERE id = 1;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
COMMIT;

Как работают блокировки (LOCKS) в PostgreSQL?
PostgreSQL поддерживает разные типы блокировок для предотвращения конфликтов при конкурентных изменениях данных:
- **Row-level locks** – блокировка отдельных строк (`SELECT FOR UPDATE`).
- **Table-level locks** – блокировка всей таблицы (`LOCK TABLE`).
- **Deadlocks (взаимные блокировки)** – ситуации, когда транзакции блокируют друг друга.

-- Блокировка строки для предотвращения изменения другими транзакциями
SELECT * FROM accounts WHERE id = 1 FOR UPDATE;

-- Полная блокировка таблицы
LOCK TABLE accounts IN EXCLUSIVE MODE;

В каких случаях может возникнуть Deadlock и как его предотвратить?
Deadlock – это ситуация, когда две или более транзакций ждут друг друга, вызывая бесконечную блокировку.
Как предотвратить Deadlock:
- Захватывать ресурсы в одном и том же порядке во всех транзакциях.
- Ограничить время ожидания (`SET lock_timeout`).
- Использовать `NOWAIT` или `SKIP LOCKED` для избежания ожидания заблокированных строк.

-- Установка тайм-аута для блокировки
SET lock_timeout = '5s';

-- Использование NOWAIT для немедленного выхода при блокировке
SELECT * FROM accounts WHERE id = 1 FOR UPDATE NOWAIT;

-- Использование SKIP LOCKED для обработки только доступных строк
SELECT * FROM accounts WHERE status = 'pending' FOR UPDATE SKIP LOCKED;

Как узнать, какие процессы блокируют другие (`pg_stat_activity`)?
PostgreSQL предоставляет `pg_stat_activity` для мониторинга активных процессов и блокировок.

-- Проверка активных процессов и блокировок
SELECT pid, state, query FROM pg_stat_activity WHERE state = 'active';

-- Поиск заблокированных процессов
SELECT blocking_pid, blocked_pid, query FROM pg_locks JOIN pg_stat_activity ON pid = blocked_pid;

Грамотное управление транзакциями и блокировками позволяет избежать потери данных и повысить производительность работы PostgreSQL в многопользовательской среде.
 
Работа с JSON и массивами в PostgreSQL
PostgreSQL поддерживает сложные структуры данных, такие как JSON и массивы, что делает его удобным для хранения неструктурированных данных.
В чем разница между JSON и JSONB? Когда использовать JSONB?
PostgreSQL поддерживает два типа JSON-данных:
- **JSON** – текстовый формат хранения данных (медленнее при поиске, но точный порядок сохраняется).
- **JSONB** – бинарное представление JSON (оптимизировано для поиска и индексации, но изменяет порядок полей).

-- Создание таблицы с JSON и JSONB
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name TEXT,
    attributes JSONB
);

-- Вставка данных в JSONB
INSERT INTO products (name, attributes) VALUES ('Phone', '{"brand": "Apple", "model": "iPhone 13"}'::jsonb);

-- Поиск по JSONB
SELECT * FROM products WHERE attributes @> '{"brand": "Apple"}';

Как хранить массивы в PostgreSQL и как с ними работать?
PostgreSQL позволяет хранить массивы в таблицах и выполнять операции над ними.

-- Создание таблицы с массивом
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name TEXT,
    grades INTEGER[]
);

-- Вставка данных
INSERT INTO students (name, grades) VALUES ('Alice', ARRAY[85, 90, 78]);

-- Поиск студентов с оценкой 90
SELECT * FROM students WHERE 90 = ANY(grades);

Как выполнить быстрый поиск по JSONB?
Для ускорения поиска по JSONB используется индекс GIN.

-- Создание GIN индекса для JSONB
CREATE INDEX idx_products_attributes ON products USING GIN (attributes);

-- Поиск товаров по вложенному значению
SELECT * FROM products WHERE attributes @> '{"model": "iPhone 13"}';

Какие индексы работают с JSONB?
Для ускорения запросов к JSONB используются индексы:
- **GIN (Generalized Inverted Index)** – самый эффективный индекс для JSONB.
- **B-Tree** – используется для хранения и поиска по определённым ключам.
Как проверить, содержит ли JSONB определенный ключ?

-- Поиск всех товаров, у которых есть ключ "brand"
SELECT * FROM products WHERE attributes ? 'brand';

Как извлекать данные из JSONB (`->`, `->>`, `jsonb_each`)?
PostgreSQL предоставляет несколько операторов для работы с JSONB:
- **`->`** – извлекает вложенный JSON-объект или массив.
- **`->>`** – извлекает строковое представление значения.
- **`jsonb_each()`** – разворачивает JSONB в таблицу.

-- Извлечение значения из JSONB
SELECT attributes->'brand' FROM products;

-- Извлечение строкового значения
SELECT attributes->>'brand' FROM products;

-- Разворачивание JSONB в таблицу
SELECT * FROM jsonb_each('{"brand": "Apple", "model": "iPhone 13"}'::jsonb);

Использование JSONB и массивов в PostgreSQL позволяет эффективно работать с неструктурированными данными и выполнять сложные запросы с высокой скоростью.
 
Хранимые процедуры, триггеры и функции в PostgreSQL
PostgreSQL поддерживает хранимые процедуры, триггеры и функции, которые позволяют автоматизировать обработку данных и выполнять сложные операции внутри базы.
Как создать и использовать хранимую процедуру?
Хранимые процедуры (`PROCEDURE`) позволяют выполнять SQL-команды внутри базы данных и могут изменять данные без необходимости возвращать результат.

-- Создание хранимой процедуры
CREATE PROCEDURE increase_salary(emp_id INT, percent NUMERIC)
LANGUAGE plpgsql
AS $$
BEGIN
  UPDATE employees SET salary = salary * (1 + percent / 100) WHERE id = emp_id;
END;
$$;

-- Вызов хранимой процедуры
CALL increase_salary(1, 10);

В чем разница между FUNCTION и PROCEDURE?
Разница между `FUNCTION` и `PROCEDURE` в PostgreSQL:
- **FUNCTION** возвращает значение и может использоваться в SQL-запросах.
- **PROCEDURE** не возвращает значение и вызывается командой `CALL`.
Как создать функцию в PostgreSQL?

-- Создание функции, которая возвращает зарплату сотрудника
CREATE FUNCTION get_salary(emp_id INT) RETURNS NUMERIC AS $$
DECLARE
    salary NUMERIC;
BEGIN
    SELECT employees.salary INTO salary FROM employees WHERE id = emp_id;
    RETURN salary;
END;
$$ LANGUAGE plpgsql;

-- Вызов функции
SELECT get_salary(1);

Что такое триггеры и как они работают?
Триггеры (`TRIGGER`) позволяют автоматически выполнять SQL-команды при изменении данных в таблице (INSERT, UPDATE, DELETE).

-- Создание таблицы для логирования изменений
CREATE TABLE employee_changes (
    change_id SERIAL PRIMARY KEY,
    emp_id INT,
    change_time TIMESTAMP DEFAULT NOW(),
    action TEXT
);

-- Создание функции триггера
CREATE FUNCTION log_employee_changes() RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO employee_changes (emp_id, action) VALUES (NEW.id, 'Updated');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Создание триггера, который срабатывает при обновлении данных в таблице employees
CREATE TRIGGER employee_update_trigger
AFTER UPDATE ON employees
FOR EACH ROW EXECUTE FUNCTION log_employee_changes();

Как работают event triggers?
Event triggers позволяют реагировать на глобальные события в базе данных, такие как `CREATE TABLE` или `DROP TABLE`.

-- Создание функции для event trigger
CREATE FUNCTION log_table_creation() RETURNS event_trigger AS $$
BEGIN
    RAISE NOTICE 'Таблица создана: %', tg_event;
END;
$$ LANGUAGE plpgsql;

-- Создание триггера на создание таблиц
CREATE EVENT TRIGGER table_creation_trigger
ON ddl_command_start
WHEN TAG IN ('CREATE TABLE')
EXECUTE FUNCTION log_table_creation();

Использование хранимых процедур, триггеров и функций в PostgreSQL позволяет автоматизировать обработку данных и улучшить производительность системы.
 
Репликация, бэкапы и восстановление в PostgreSQL
PostgreSQL поддерживает различные методы репликации, резервного копирования и восстановления данных, что помогает обеспечивать отказоустойчивость и защиту информации.
Какие существуют типы репликации в PostgreSQL?
PostgreSQL поддерживает несколько типов репликации:
- **Потоковая репликация (Streaming Replication)** – передача WAL-журналов от ведущего сервера к реплике.
- **Логическая репликация (Logical Replication)** – репликация отдельных таблиц через публикации и подписки.
- **Slony-I** – сторонний инструмент для асинхронной репликации.
- **BDR (Bi-Directional Replication)** – двусторонняя репликация для мульти-мастер-систем.

-- Настройка потоковой репликации (на мастере)
ALTER SYSTEM SET wal_level = 'replica';
ALTER SYSTEM SET max_wal_senders = 5;
SELECT pg_reload_conf();

Как сделать бэкап базы данных?
PostgreSQL поддерживает несколько способов резервного копирования:
- **pg_dump** – создание логического дампа базы данных.
- **pg_basebackup** – поблочное копирование данных для репликации.
- **WAL Archiving** – журналирование всех изменений базы данных.

-- Создание логического дампа базы
pg_dump -U postgres -F c -b -v -f "backup.dump" my_database;

-- Создание полного физического бэкапа базы
pg_basebackup -D /var/lib/postgresql/backup -Fp -Xs -P -U replication;

Как восстановить базу данных из бэкапа?
Методы восстановления базы данных в PostgreSQL:
- **pg_restore** – восстановление базы из логического дампа.
- **PITR (Point-in-Time Recovery)** – восстановление базы до определенного момента времени.

-- Восстановление базы из логического дампа
pg_restore -U postgres -d my_database "backup.dump";

-- Восстановление базы с использованием PITR
recovery_target_time = '2024-03-01 12:00:00'

Что такое WAL (Write-Ahead Logging) и как оно работает?
WAL (Write-Ahead Logging) – механизм записи изменений в журнал перед их применением к основной базе, что повышает надежность и позволяет использовать репликацию.

-- Включение WAL-архивации
ALTER SYSTEM SET archive_mode = 'on';
ALTER SYSTEM SET archive_command = 'cp %p /var/lib/postgresql/wal_archive/%f';
SELECT pg_reload_conf();

Как работает PITR (Point-in-Time Recovery)?
PITR позволяет откатить базу данных к определенному моменту времени, используя WAL-логи.

-- Указать время восстановления в recovery.conf
recovery_target_time = '2024-03-01 12:00:00';

-- Запустить сервер в режиме восстановления
pg_ctl -D /var/lib/postgresql/data -l logfile start

Использование репликации, бэкапов и восстановления данных в PostgreSQL помогает обеспечить отказоустойчивость и защиту данных.
SQL Cheat Sheet с примерами
Категория (🔹 Уровень)	SQL-команды	Объяснение	Пример
🟢 Таблицы	CREATE TABLE table_name (
    id INT PRIMARY KEY,
    name VARCHAR NOT NULL,
    price INT DEFAULT 0
);
ALTER TABLE table_name RENAME TO new_table_name;
DROP TABLE table_name;
TRUNCATE TABLE table_name;	CREATE TABLE создаёт новую таблицу.
ALTER TABLE позволяет переименовать таблицу.
DROP TABLE удаляет таблицу и её данные.
TRUNCATE TABLE удаляет все записи, но сохраняет структуру.	CREATE TABLE создаёт новую таблицу.
Пример:
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);
```
🟡 Индексы	CREATE INDEX index_name ON table_name (column1, column2);
CREATE UNIQUE INDEX unique_index_name ON table_name (column1, column2);
DROP INDEX index_name;	CREATE INDEX создаёт индекс для ускорения поиска.
CREATE UNIQUE INDEX создаёт уникальный индекс, исключая дублирование значений.
DROP INDEX удаляет индекс.	CREATE INDEX создаёт индекс для ускорения поиска.
Пример:
```sql
CREATE INDEX idx_users_email ON users(email);
```
🔴 Триггеры	CREATE OR MODIFY TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE
ON table_name FOR EACH ROW
EXECUTE stored_procedure;
DROP TRIGGER trigger_name;	CREATE TRIGGER создаёт триггер, который автоматически выполняется при INSERT, UPDATE или DELETE.
DROP TRIGGER удаляет триггер.	CREATE TRIGGER создаёт триггер, который автоматически выполняется при INSERT, UPDATE или DELETE.
Пример:
```sql
CREATE TRIGGER before_insert_users
BEFORE INSERT ON users
FOR EACH ROW
EXECUTE FUNCTION check_user_email();
```

🟢 Поля	ALTER TABLE table_name ADD column_name DATATYPE;
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;
ALTER TABLE table_name DROP COLUMN column_name;	ALTER TABLE ADD добавляет новое поле в таблицу.
ALTER TABLE RENAME COLUMN переименовывает существующее поле.
ALTER TABLE DROP COLUMN удаляет поле из таблицы.	ALTER TABLE ADD добавляет новое поле в таблицу.
Пример:
```sql
ALTER TABLE users ADD COLUMN age INT;
```
🟢 Записи	INSERT INTO table_name (column1, column2) VALUES (value1, value2);
INSERT INTO table_name (column1, column2) VALUES (value1, value2), (value3, value4);
INSERT INTO table1 (column1, column2) SELECT column1, column2 FROM table2;
UPDATE table_name SET column1 = new_value WHERE condition;
DELETE FROM table_name WHERE condition;
DELETE FROM table_name;	INSERT INTO добавляет новые записи в таблицу.
UPDATE обновляет существующие записи.
DELETE FROM удаляет записи по заданному условию.
DELETE FROM без WHERE удаляет все записи.	INSERT INTO добавляет новые записи в таблицу.
Пример:
```sql
INSERT INTO users (name, email) VALUES ('Alex', 'alex@example.com');
```

🟡 Ограничения	ALTER TABLE table_name ADD CONSTRAINT constraint_name;
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
CREATE TABLE table_name (
    column1 INT,
    column2 INT,
    PRIMARY KEY (column1, column2)
);
CREATE TABLE table_name (
    column1 INT PRIMARY KEY,
    column2 INT,
    FOREIGN KEY (column2) REFERENCES other_table(column1)
);
CREATE TABLE table_name (
    column1 INT,
    column2 INT UNIQUE
);
CREATE TABLE table_name (
    column1 INT,
    column2 INT,
    CHECK (column1 > 0 AND column1 >= column2)
);
CREATE TABLE table_name (
    column1 INT PRIMARY KEY,
    column2 VARCHAR NOT NULL
);	PRIMARY KEY создаёт уникальный идентификатор для строки.
FOREIGN KEY создаёт связь между таблицами.
UNIQUE гарантирует уникальность значений в колонке.
CHECK накладывает условие на значения в колонке.
NOT NULL запрещает пустые значения.	PRIMARY KEY создаёт уникальный идентификатор для строки.
Пример:
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    amount DECIMAL(10,2) CHECK (amount > 0)
);
```
🟢 Выборка данных	SELECT column1, column2 FROM table_name;
SELECT * FROM table_name;
SELECT DISTINCT column1 FROM table_name;
SELECT * FROM table_name ORDER BY column1 ASC (или DESC);
SELECT * FROM table_name ORDER BY column1 LIMIT 5 OFFSET 10;	SELECT выбирает данные из таблицы.
SELECT DISTINCT выбирает только уникальные значения.
ORDER BY сортирует данные по возрастанию или убыванию.
LIMIT ограничивает количество выводимых записей.	SELECT выбирает данные из таблицы.
Пример:
```sql
SELECT name, email FROM users WHERE name LIKE 'A%';
```
🟢 Условия	SELECT column1 FROM table_name WHERE condition;
SELECT column1 FROM table_name WHERE column2 LIKE '%pattern%';
SELECT column1 FROM table_name WHERE column2 IN (value1, value2);
SELECT column1 FROM table_name WHERE column2 BETWEEN value1 AND value2;
SELECT column1 FROM table_name WHERE column2 IS NOT NULL;	WHERE фильтрует данные по заданному условию.
LIKE используется для поиска по шаблону.
IN проверяет наличие значения в списке.
BETWEEN проверяет, находится ли значение в заданном диапазоне.
IS NOT NULL фильтрует записи с непустыми значениями.	WHERE фильтрует данные по заданному условию.
Пример:
```sql
SELECT * FROM users WHERE age BETWEEN 18 AND 30;
```
🟡 Агрегатные функции	SELECT COUNT(*) FROM table_name;
SELECT MAX(column1) FROM table_name;
SELECT MIN(column1) FROM table_name;
SELECT AVG(column1) FROM table_name;
SELECT column1, aggregate(column2) FROM table_name GROUP BY column1;
SELECT column1, aggregate(column2) FROM table_name GROUP BY column1 HAVING condition;	COUNT() возвращает количество записей.
MAX() и MIN() находят максимальное и минимальное значения.
AVG() вычисляет среднее значение.
GROUP BY группирует записи.
HAVING фильтрует сгруппированные результаты.	COUNT() возвращает количество записей.
Пример:
```sql
SELECT COUNT(*) FROM users;
```
🔴 Комбинации выборок	SELECT column1, column2 FROM table1
UNION [ALL]
SELECT column1, column2 FROM table2;
SELECT column1, column2 FROM table1
INTERSECT
SELECT column1, column2 FROM table2;
SELECT column1, column2 FROM table1
MINUS
SELECT column1, column2 FROM table2;	UNION объединяет результаты двух запросов.
INTERSECT возвращает только пересекающиеся результаты.
MINUS вычитает один запрос из другого.	UNION объединяет результаты двух запросов.
Пример:
```sql
SELECT name FROM users WHERE age < 25
UNION
SELECT name FROM users WHERE age > 50;
```
🔴 Соединение таблиц	SELECT t1.column1, t2.column2 FROM table1 t1
INNER JOIN table2 t2 ON condition;
SELECT t1.column1, t2.column2 FROM table1 t1
LEFT JOIN table2 t2 ON condition;
SELECT t1.column1, t2.column2 FROM table1 t1
RIGHT JOIN table2 t2 ON condition;
SELECT t1.column1, t2.column2 FROM table1 t1
FULL OUTER JOIN table2 t2 ON condition;
SELECT t1.column1, t2.column2 FROM table1 t1
CROSS JOIN table2 t2;	INNER JOIN выбирает совпадающие записи из двух таблиц.
LEFT JOIN выбирает все записи из левой таблицы и совпадающие из правой.
RIGHT JOIN выбирает все записи из правой таблицы и совпадающие из левой.
FULL OUTER JOIN выбирает все записи из обеих таблиц.
CROSS JOIN возвращает декартово произведение двух таблиц.	INNER JOIN выбирает совпадающие записи из двух таблиц.
Пример:
```sql
SELECT users.name, orders.amount
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```
🔴 Представления	CREATE VIEW view_name(column1, column2) AS 
SELECT column1, column2 FROM table_name;
CREATE VIEW view_name(column1, column2) AS 
SELECT column1, column2 FROM table_name 
WITH [CASCADED|LOCAL] CHECK OPTION;
CREATE RECURSIVE VIEW view_name AS 
SELECT statement -- anchor part
UNION [ALL] 
SELECT statement -- recursive part;
CREATE TEMPORARY VIEW view_name AS 
SELECT column1, column2 FROM table_name;
DROP VIEW view_name;	CREATE VIEW создаёт виртуальную таблицу на основе запроса.
CREATE RECURSIVE VIEW создаёт рекурсивное представление.
DROP VIEW удаляет представление.	CREATE VIEW создаёт виртуальную таблицу на основе запроса.
Пример:
```sql
CREATE VIEW user_orders AS
SELECT users.name, orders.amount FROM users
JOIN orders ON users.id = orders.user_id;
```
 
SQL: Вопросы на собеседовании и ответы
1. В чем разница между DELETE, TRUNCATE и DROP?


✅ **DELETE**: Удаляет записи из таблицы, но структура остаётся. Можно использовать WHERE.
✅ **TRUNCATE**: Удаляет все записи, но быстрее, чем DELETE. Структура остаётся.
✅ **DROP**: Удаляет таблицу полностью, включая структуру.

Пример:
```sql
DELETE FROM users WHERE age < 18;
TRUNCATE TABLE users;
DROP TABLE users;
```
2. Что такое первичный и внешний ключи?


✅ **PRIMARY KEY**: Уникальный идентификатор строки.
✅ **FOREIGN KEY**: Связывает одну таблицу с другой.

Пример:
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);

CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id)
);
```
3. Что такое нормализация в базе данных?


✅ Нормализация – это процесс оптимизации структуры базы данных для уменьшения дублирования данных.

🔹 **1NF (Первая нормальная форма)**: Удаляем повторяющиеся группы данных.
🔹 **2NF (Вторая нормальная форма)**: Каждое поле зависит от первичного ключа.
🔹 **3NF (Третья нормальная форма)**: Убираем транзитивные зависимости.

Пример:
**Плохо:** Таблица с повторяющимися данными  
**Хорошо:** Разделение данных на несколько связанных таблиц

4. Как работает индекс в SQL?


✅ Индекс ускоряет поиск данных, создавая специальную структуру.

Пример:
```sql
CREATE INDEX idx_users_email ON users(email);
```

⚠️ **Важно:** Индексы ускоряют SELECT, но замедляют INSERT/UPDATE, так как таблице приходится обновлять индекс.
5. Разница между INNER JOIN, LEFT JOIN и RIGHT JOIN?


✅ **INNER JOIN**: Выбирает только совпадающие записи из обеих таблиц.  
✅ **LEFT JOIN**: Выбирает все записи из левой таблицы + совпадающие из правой.  
✅ **RIGHT JOIN**: Выбирает все записи из правой таблицы + совпадающие из левой.  

Пример:
```sql
SELECT users.name, orders.amount
FROM users
LEFT JOIN orders ON users.id = orders.user_id;
```
6. Что такое подзапрос (Subquery)?


✅ Подзапрос — это вложенный SELECT внутри другого запроса.

Пример:
```sql
SELECT name FROM users WHERE id IN (
    SELECT user_id FROM orders WHERE amount > 1000
);
```

⚠️ **Важно:** Подзапросы могут быть медленными, иногда лучше использовать JOIN.
7. Как избежать SQL-инъекций?


✅ **Используйте подготовленные запросы (Prepared Statements)**  
✅ **Не храните пароли в открытом виде – используйте хеширование (bcrypt, SHA256)**  
✅ **Ограничивайте права пользователей (например, только SELECT для чтения)**  

Пример безопасного запроса в PostgreSQL:
```sql
PREPARE stmt FROM 'SELECT * FROM users WHERE email = ?';
EXECUTE stmt USING 'alex@example.com';
```
 
PostgreSQL: Вопросы на собеседовании и ответы
1. Чем PostgreSQL отличается от других СУБД (MySQL, Oracle, MS SQL Server)?

PostgreSQL — это мощная объектно-реляционная база данных с поддержкой ACID-транзакций, расширяемости и сложных типов данных.

🔹 **Основные отличия PostgreSQL:**
- **Расширяемость**: поддержка пользовательских функций, хранимых процедур, типов данных (JSONB, XML, ARRAY, HSTORE)
- **Поддержка NoSQL**: JSONB позволяет хранить и быстро искать данные, как в NoSQL
- **ACID-соответствие**: строгая поддержка транзакций по сравнению с MySQL
- **Мощный планировщик запросов**: PostgreSQL использует EXPLAIN ANALYZE для оптимизации запросов
- **Лучше масштабируется**: Поддерживает репликацию, шардинг, партиционирование


2. Как посмотреть список всех баз данных в PostgreSQL?

В PostgreSQL можно получить список баз данных несколькими способами:

✅ **В командной строке (psql):**
```sql
\l
```

✅ **Через SQL-запрос:**
```sql
SELECT datname FROM pg_database;
```


3. Как создать и удалить базу данных в PostgreSQL?

Для создания базы данных используем команду:

```sql
CREATE DATABASE mydb;
```

Удалить базу данных можно так:

```sql
DROP DATABASE mydb;
```

⚠️ **Важно:** Нельзя удалить активную базу, сначала нужно переключиться на другую (`\c postgres`).


4. Как создать индекс в PostgreSQL? Какие бывают индексы?

Индексы ускоряют поиск, но замедляют INSERT/UPDATE. PostgreSQL поддерживает:

✅ **B-Tree (по умолчанию)** – используется для `=`, `<`, `>`  
✅ **GIN (Generalized Inverted Index)** – подходит для JSONB и full-text search  
✅ **GiST (Generalized Search Tree)** – используется для геоданных  
✅ **BRIN (Block Range Index)** – эффективен для больших таблиц  
✅ **Hash Index** – быстрее B-Tree, но поддерживает только `=`  

**Пример создания индекса:**

```sql
CREATE INDEX idx_users_email ON users(email);
```


5. Чем JSON отличается от JSONB?

PostgreSQL поддерживает два типа хранения JSON:

✅ **JSON** – хранится в текстовом формате, порядок ключей сохраняется, но медленный для поиска.  
✅ **JSONB** – хранится в бинарном формате, быстрее в поиске, но не сохраняет порядок ключей.

**Пример работы с JSONB:**

```sql
SELECT data->>'name' FROM users WHERE data->>'age' = '30';
```


6. Как работает FULL-TEXT SEARCH в PostgreSQL?

Full-Text Search (FTS) позволяет искать слова в текстах, учитывая морфологию.

**Пример поиска:**

```sql
SELECT * FROM articles WHERE to_tsvector(content) @@ to_tsquery('postgres & SQL');
```

**Создание индекса для быстрого поиска:**

```sql
CREATE INDEX idx_articles_content ON articles USING GIN(to_tsvector('english', content));
```


7. Как работает EXPLAIN ANALYZE?

`EXPLAIN ANALYZE` помогает понять, как PostgreSQL выполняет запрос.

**Пример:**

```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';
```

Выдаст план выполнения, включая **затраты времени, индексы, количество строк**.


8. Как работают транзакции в PostgreSQL?

Транзакция — это набор SQL-команд, выполняемых атомарно (ACID).

**Пример транзакции:**

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

❌ **Если произошла ошибка, можно откатить:**

```sql
ROLLBACK;
```


9. Как посмотреть активные соединения в PostgreSQL?

Чтобы увидеть текущие соединения:

```sql
SELECT * FROM pg_stat_activity;
```

Если нужно завершить зависший процесс:

```sql
SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE state = 'active';
```


10. Как защитить PostgreSQL от SQL-инъекций?

✅ **Используйте подготовленные запросы (Prepared Statements):**

```sql
PREPARE stmt FROM 'SELECT * FROM users WHERE email = $1';
EXECUTE stmt USING 'alex@example.com';
```

✅ **Не храните пароли в открытом виде – используйте хеширование:**

```sql
SELECT crypt('password123', gen_salt('bf'));
```

✅ **Ограничивайте права пользователей:**

```sql
REVOKE ALL ON users FROM public;
```



 
 
 
 
Основы HTML
HTML (HyperText Markup Language) — это язык разметки, используемый для создания веб-страниц. Он описывает структуру документа с помощью тегов.
Что такое HTML и зачем он нужен?
HTML используется для разметки контента на веб-страницах. Каждый элемент в HTML обозначается с помощью тегов.

// Простейшая HTML-страница
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Пример HTML</title>
</head>
<body>
    <h1>Привет, мир!</h1>
    <p>Это мой первый HTML-документ.</p>
</body>
</html>

Какие есть основные теги в HTML?
Основные теги HTML:
- `<html>` — корневой элемент документа.
- `<head>` — содержит мета-информацию о странице.
- `<body>` — содержит отображаемый контент.
- `<h1> - <h6>` — заголовки.
- `<p>` — параграф текста.
- `<a>` — ссылка.
- `<img>` — изображение.
- `<ul>` / `<ol>` — списки.
- `<table>` — таблица.
Что такое атрибуты в HTML и какие бывают?
Атрибуты в HTML задают дополнительные параметры для тегов. Они записываются внутри открывающего тега.

// Пример использования атрибутов
<a href="https://example.com" target="_blank">Посетить сайт</a>
<img src="image.jpg" alt="Описание изображения">

В чем разница между блочными и строчными элементами?
- **Блочные элементы** (`<div>`, `<p>`, `<h1>` и др.) занимают всю ширину контейнера.
- **Строчные элементы** (`<span>`, `<a>`, `<strong>`) занимают только нужное пространство.

// Пример блочного и строчного элемента
<div style="background: lightgray;">Блочный элемент</div>
<span style="background: yellow;">Строчный элемент</span>

Как правильно структурировать HTML-документ?
Хорошо структурированный HTML-документ включает следующие секции:
- `<!DOCTYPE html>` — определяет версию HTML.
- `<html>` — корневой элемент.
- `<head>` — мета-информация, стили, скрипты.
- `<body>` — основной контент страницы.

// Пример правильно структурированного HTML-документа
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Структура HTML</title>
</head>
<body>
    <header>
        <h1>Заголовок</h1>
    </header>
    <main>
        <p>Основной контент страницы.</p>
    </main>
    <footer>
        <p>Контактная информация</p>
    </footer>
</body>
</html>

Основы HTML включают структуру документа, основные теги, блочные и строчные элементы, а также использование атрибутов. Знание этих принципов — ключ к созданию правильных веб-страниц.
 
Семантический HTML
Семантический HTML — это использование специальных тегов, которые отражают смысл содержимого страницы. Он помогает поисковым системам, браузерам и вспомогательным технологиям лучше интерпретировать контент.
Что такое семантические теги?
Семантические теги в HTML5 дают четкое представление о содержимом веб-страницы. Они заменяют `<div>` и `<span>`, делая структуру кода более понятной.

// Пример семантических тегов
<header>Заголовок сайта</header>
<nav>Меню сайта</nav>
<main>
    <section>Основной контент</section>
    <article>Новостной блок</article>
</main>
<footer>Подвал сайта</footer>

В чем разница между <div> и <section>?
- **`<div>`** — универсальный контейнер, не несет смысловой нагрузки.
- **`<section>`** — семантический блок, объединяющий контент по смыслу.

// Использование div (менее семантично)
<div class="news">
    <h2>Заголовок новости</h2>
    <p>Текст новости</p>
</div>

// Использование section (семантично)
<section>
    <h2>Заголовок новости</h2>
    <p>Текст новости</p>
</section>

Зачем использовать семантическую разметку?
Преимущества семантического HTML:
- Улучшает **SEO**, помогая поисковым системам лучше индексировать сайт.
- Улучшает **доступность** для пользователей с ограниченными возможностями.
- Делает код **более читаемым и поддерживаемым**.
Какие семантические теги существуют в HTML5?
Основные семантические теги в HTML5:
- `<header>` — заголовок страницы или раздела.
- `<nav>` — меню навигации.
- `<main>` — основной контент страницы.
- `<section>` — смысловой блок контента.
- `<article>` — независимый блок контента (новости, статьи).
- `<aside>` — боковая панель.
- `<footer>` — подвал страницы.

// Пример использования семантических тегов
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Семантический HTML</title>
</head>
<body>
    <header>
        <h1>Название сайта</h1>
    </header>
    <nav>
        <ul>
            <li><a href="#">Главная</a></li>
            <li><a href="#">О нас</a></li>
        </ul>
    </nav>
    <main>
        <section>
            <h2>Новости</h2>
            <article>
                <h3>Заголовок статьи</h3>
                <p>Текст статьи...</p>
            </article>
        </section>
    </main>
    <footer>
        <p>Контакты и информация</p>
    </footer>
</body>
</html>

Использование семантических тегов улучшает доступность, SEO и делает код более структурированным. Рекомендуется заменять `<div>` и `<span>` там, где есть подходящие семантические теги.
 
Формы и работа с вводом пользователя
Формы в HTML используются для сбора данных от пользователей. Они могут содержать различные поля ввода, кнопки и элементы управления.
Как создать HTML-форму?
HTML-форма создается с помощью тега `<form>`, который содержит элементы ввода (`<input>`, `<textarea>`, `<select>`, `<button>`).

// Простая HTML-форма
<form action="/submit" method="POST">
    <label for="name">Имя:</label>
    <input type="text" id="name" name="name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    
    <button type="submit">Отправить</button>
</form>

Какие бывают типы input?
Основные типы `<input>` в HTML:
- `text` — поле для ввода текста.
- `email` — поле для ввода email (с проверкой формата).
- `password` — поле для ввода пароля (скрытый ввод).
- `number` — числовое поле.
- `checkbox` — флажок (много вариантов).
- `radio` — радиокнопка (один вариант).
- `file` — загрузка файла.
- `date`, `time`, `datetime-local` — ввод даты и времени.

// Разные типы полей ввода
<form>
    <input type="text" placeholder="Текст">
    <input type="email" placeholder="Email">
    <input type="password" placeholder="Пароль">
    <input type="number" placeholder="Число">
    <input type="date">
    <input type="checkbox"> Чекбокс
    <input type="radio" name="group"> Радиокнопка
</form>

Что делает label и почему его важно использовать?
Тег `<label>` связывает подпись с полем ввода, улучшая доступность и удобство использования.

// Использование label
<form>
    <label for="username">Имя пользователя:</label>
    <input type="text" id="username" name="username">
</form>

Как использовать select и textarea?
Тег `<select>` создает выпадающий список, а `<textarea>` используется для ввода многострочного текста.

// Выпадающий список и текстовая область
<form>
    <label for="country">Выберите страну:</label>
    <select id="country" name="country">
        <option value="ru">Россия</option>
        <option value="us">США</option>
        <option value="de">Германия</option>
    </select>
    
    <label for="message">Сообщение:</label>
    <textarea id="message" name="message" rows="4"></textarea>
</form>

Как сделать autocomplete и datalist?
Атрибут `autocomplete` позволяет браузеру предлагать варианты ввода, а `<datalist>` определяет список возможных значений.

// Пример использования autocomplete и datalist
<form>
    <input type="text" name="city" list="cities" placeholder="Введите город">
    <datalist id="cities">
        <option value="Москва">
        <option value="Санкт-Петербург">
        <option value="Казань">
    </datalist>
</form>

Как работает fieldset и legend?
`<fieldset>` группирует элементы формы, а `<legend>` задает заголовок группы.

// Пример использования fieldset и legend
<form>
    <fieldset>
        <legend>Личная информация</legend>
        <label for="fname">Имя:</label>
        <input type="text" id="fname" name="fname">
        
        <label for="lname">Фамилия:</label>
        <input type="text" id="lname" name="lname">
    </fieldset>
</form>

Формы в HTML позволяют взаимодействовать с пользователем. Использование семантических тегов `<label>`, `<fieldset>` и атрибутов `required`, `placeholder` улучшает пользовательский опыт и доступность.
 
Гиперссылки и работа с ресурсами
Гиперссылки позволяют переходить между страницами, а ресурсы (изображения, шрифты, стили) улучшают внешний вид и функциональность сайта.
Как правильно создать ссылку <a>?
Тег `<a>` создаёт ссылку на другую страницу. Атрибут `href` указывает путь к ресурсу.

// Простейшая ссылка
<a href="https://example.com">Перейти на сайт</a>

// Ссылка, открывающаяся в новой вкладке
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Открыть в новой вкладке</a>

В чем разница между относительными и абсолютными путями?
- **Абсолютный путь** — полный URL (например, `https://example.com/page`).
- **Относительный путь** — путь относительно текущего документа (`/about`, `../images/photo.jpg`).

// Абсолютная ссылка
<a href="https://example.com/about">О компании</a>

// Относительная ссылка
<a href="/about">О компании</a>

Как правильно вставлять изображения в HTML?
Тег `<img>` используется для вставки изображений. Атрибут `alt` обязателен для доступности.

// Вставка изображения
<img src="image.jpg" alt="Описание изображения">

// Указание ширины и высоты
<img src="image.jpg" alt="Описание" width="300" height="200">

Что такое favicon и как его добавить?
Favicon — это иконка веб-сайта, отображающаяся на вкладке браузера.

// Подключение favicon
<link rel="icon" type="image/png" href="favicon.png">

Как подключить шрифты в HTML?
Шрифты можно подключать с помощью Google Fonts или через `@font-face`.

// Подключение Google Fonts
<link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">

// Использование шрифта
<style>
    body {
        font-family: 'Roboto', sans-serif;
    }
</style>

Как добавить иконки с FontAwesome?
FontAwesome — это библиотека иконок, подключаемая через CDN.

// Подключение FontAwesome
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

// Использование иконки
<i class="fa-solid fa-user"></i>

Гиперссылки и ресурсы помогают организовать навигацию и стилизацию веб-страницы. Использование правильных путей, фавиконов, шрифтов и иконок делает сайт удобнее.
 
Таблицы в HTML
Таблицы в HTML используются для представления данных в строках и столбцах. Они создаются с помощью тега `<table>` и его дочерних элементов.
Как создать таблицу в HTML?
Основные теги для работы с таблицами:
- `<table>` — создаёт таблицу.
- `<tr>` — строка таблицы.
- `<th>` — заголовочная ячейка (жирный текст по умолчанию).
- `<td>` — обычная ячейка.

// Пример таблицы в HTML
<table border="1">
    <tr>
        <th>Имя</th>
        <th>Возраст</th>
    </tr>
    <tr>
        <td>Иван</td>
        <td>25</td>
    </tr>
    <tr>
        <td>Мария</td>
        <td>30</td>
    </tr>
</table>

Как объединять ячейки в таблице?
Используются атрибуты:
- `colspan` — объединяет несколько столбцов.
- `rowspan` — объединяет несколько строк.

// Объединение ячеек в таблице
<table border="1">
    <tr>
        <th colspan="2">Объединённый заголовок</th>
    </tr>
    <tr>
        <td rowspan="2">Объединение строк</td>
        <td>Данные 1</td>
    </tr>
    <tr>
        <td>Данные 2</td>
    </tr>
</table>

Как стилизовать таблицу с CSS?
Для улучшения внешнего вида таблицы используются CSS-стили. Можно изменить отступы, границы и цвет фона.

// Стилизация таблицы с CSS
<style>
    table {
        width: 100%;
        border-collapse: collapse;
    }
    th, td {
        border: 1px solid black;
        padding: 8px;
        text-align: left;
    }
    th {
        background-color: lightgray;
    }
</style>

Как сделать адаптивную таблицу?
Для адаптивности можно использовать `overflow: auto;` или `display: block;` для скроллинга таблицы на маленьких экранах.

// Адаптивная таблица с прокруткой
<div style="overflow-x: auto;">
    <table border="1">
        <tr>
            <th>Заголовок 1</th>
            <th>Заголовок 2</th>
            <th>Заголовок 3</th>
        </tr>
        <tr>
            <td>Данные 1</td>
            <td>Данные 2</td>
            <td>Данные 3</td>
        </tr>
    </table>
</div>

Таблицы в HTML позволяют отображать данные в удобном формате. Объединение ячеек, стилизация и адаптивность делают их более удобными для восприятия.

Работа с мультимедиа в HTML
HTML поддерживает вставку мультимедийных элементов, таких как изображения, аудио и видео.
Для этого используются специальные теги.
Как вставить изображение в HTML?
Тег <img> используется для вставки изображений.
Важно указывать атрибут alt для доступности.

<!-- Вставка изображения -->
<img src="image.jpg" alt="Описание изображения" width="300">

Как вставить аудио в HTML?
Тег <audio> используется для встраивания аудиофайлов.
<!-- Вставка аудиофайла -->
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    Ваш браузер не поддерживает аудио.
</audio>

Как вставить YouTube-видео через <iframe>?
YouTube позволяет встраивать видео с помощью <iframe>.
<!-- Вставка YouTube-видео -->
<iframe width="560" height="315" 
        src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
        title="YouTube video player" 
        frameborder="0" allowfullscreen>
</iframe>

Как настроить параметры видео и аудио?
Основные атрибуты для <video> и <audio>:
•	controls — отображает элементы управления.
•	autoplay — запускает воспроизведение автоматически.
•	loop — зацикливает воспроизведение.
•	muted — отключает звук при старте.
<!-- Видео без звука и с автозапуском -->
<video width="400" autoplay muted loop>
    <source src="video.mp4" type="video/mp4">
</video>





Метаданные и SEO в HTML
Метаданные — это информация о веб-странице, которая не отображается пользователям, но используется поисковыми системами, браузерами и социальными сетями.
Они помогают улучшить SEO (поисковую оптимизацию) и производительность сайта.
________________________________________
1. Какие метатеги важны для SEO?
Метатеги <meta> содержат информацию о странице и находятся внутри <head>.
<head>
    <meta charset="UTF-8"> <!-- Кодировка страницы -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- Адаптивность -->
    <meta name="description" content="Краткое описание страницы (до 160 символов)"> <!-- SEO -->
    <meta name="keywords" content="HTML, SEO, метатеги"> <!-- Не всегда учитывается -->
    <meta name="author" content="Имя автора"> <!-- Автор страницы -->
</head>
Объяснение:
•	charset="UTF-8" — устанавливает кодировку символов (рекомендуется для всех страниц).
•	viewport — делает сайт адаптивным для мобильных устройств.
•	description — описание страницы для поисковых систем (важно для SEO).
•	keywords — ключевые слова (сейчас почти не учитываются Google).
•	author — имя автора страницы.



2. Как задать кодировку и язык страницы?
Кодировка UTF-8 поддерживает все языки, а язык страницы задается атрибутом lang.
<html lang="ru">
<head>
    <meta charset="UTF-8">
</head>
<body>
    <p>Привет, мир!</p>
</body>
</html>
Зачем это нужно?
•	lang="ru" — помогает поисковым системам понимать язык контента.
•	charset="UTF-8" — предотвращает проблемы с кодировкой.


3. Что такое Open Graph и Twitter Cards?
Эти метатеги нужны для правильного отображения ссылок в соцсетях (Facebook, Twitter, Telegram и др.).
<meta property="og:title" content="Название страницы">
<meta property="og:description" content="Описание для соцсетей">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="og:url" content="https://example.com/page">

<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Название страницы">
<meta name="twitter:description" content="Описание страницы">
<meta name="twitter:image" content="https://example.com/image.jpg">
Зачем это нужно?
•	og:title и twitter:title — заголовок ссылки.
•	og:description и twitter:description — описание ссылки.
•	og:image и twitter:image — изображение при публикации.

4. Как ускорить сайт с помощью метатегов?
Некоторые метатеги могут ускорить загрузку страницы.
<meta http-equiv="X-UA-Compatible" content="IE=edge"> <!-- Оптимизация для Internet Explorer -->
<meta name="robots" content="index, follow"> <!-- Разрешает поисковикам индексировать страницу -->
<meta name="theme-color" content="#ff6600"> <!-- Цвет темы для мобильных браузеров -->
Объяснение:
•	X-UA-Compatible — помогает устаревшим браузерам корректно отображать страницу.
•	robots — управляет индексацией страницы (можно запретить noindex, nofollow).
•	theme-color — изменяет цвет адресной строки в мобильных браузерах.




HTML5 API
HTML5 предоставляет мощные API, которые расширяют возможности веб-страниц.
Они позволяют работать с локальным хранилищем, геолокацией, камерой, аудио, видео, перетаскиванием файлов и многим другим.
1. Что такое LocalStorage и SessionStorage?
Эти API позволяют сохранять данные в браузере без использования серверов или базы данных.
LocalStorage (данные хранятся постоянно)
// Сохранение данных
localStorage.setItem("username", "Григорий");

// Получение данных
console.log(localStorage.getItem("username")); // "Григорий"

// Удаление данных
localStorage.removeItem("username");

SessionStorage (данные удаляются после закрытия вкладки)
sessionStorage.setItem("sessionKey", "12345");
console.log(sessionStorage.getItem("sessionKey"));
🔹 LocalStorage – данные хранятся до их удаления вручную.
🔹 SessionStorage – данные удаляются при закрытии вкладки.


2. Как работает Geolocation API?
Позволяет получать координаты пользователя.
navigator.geolocation.getCurrentPosition(position => {
    console.log("Широта:", position.coords.latitude);
    console.log("Долгота:", position.coords.longitude);
}, error => {
    console.log("Ошибка получения местоположения:", error.message);
});
🔹 Используется в мобильных приложениях, картах, погодных сервисах.
🔹 Работает только через HTTPS.
3. Как использовать Drag & Drop API?
Позволяет перетаскивать файлы или элементы.
<div id="dropzone" style="width: 200px; height: 200px; border: 2px dashed gray;">
    Перетащите сюда файл
</div>

<script>
    let dropzone = document.getElementById("dropzone");

    dropzone.addEventListener("dragover", event => {
        event.preventDefault();
    });

    dropzone.addEventListener("drop", event => {
        event.preventDefault();
        let file = event.dataTransfer.files[0];
        console.log("Файл загружен:", file.name);
    });
</script>
🔹 Используется в загрузке изображений и файлов.
🔹 Поддерживает перетаскивание элементов между областям
4. Как работает WebSockets API?
Позволяет создавать реальное соединение между сервером и клиентом (например, для чатов, онлайн-игр).
let socket = new WebSocket("wss://example.com/socket");

socket.onopen = () => {
    console.log("Соединение открыто");
    socket.send("Привет, сервер!");
};

socket.onmessage = event => {
    console.log("Сообщение от сервера:", event.data);
};

socket.onclose = () => {
    console.log("Соединение закрыто");
};
🔹 WebSockets быстрее, чем HTTP-запросы, так как соединение не разрывается.
🔹 Используется в реальном времени (чаты, игры, биржи).
5. Как использовать WebRTC API?
Позволяет создавать видеозвонки и передавать файлы без серверов.
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
    .then(stream => {
        document.getElementById("video").srcObject = stream;
    })
    .catch(error => {
        console.log("Ошибка доступа к камере:", error);
    });
🔹 WebRTC используется в видеозвонках (Zoom, Google Meet).
🔹 Работает без серверов, напрямую между пользователями.









Доступность (Accessibility, A11Y) в HTML
Доступность (A11Y) — это принцип разработки сайтов, который делает их удобными для всех пользователей, включая людей с ограниченными возможностями.
Она включает в себя использование семантического HTML, ARIA-атрибутов, навигации с клавиатуры и поддержки экранных дикторов.
1. Что такое WAI-ARIA?
WAI-ARIA (Web Accessibility Initiative – Accessible Rich Internet Applications) — это набор атрибутов,
которые помогают улучшить доступность динамических элементов на странице.
Пример кода
<button aria-label="Закрыть окно">❌</button>

🔹 aria-label — описывает элемент для пользователей экранных дикторов.
🔹 Используется, когда элемент не имеет явного текстового описания.
2. Как использовать ARIA-атрибуты для улучшения доступности?
ARIA-атрибуты помогают дополнительно описать элементы, которые могут быть сложными для понимания экранными дикторами.
Основные ARIA-атрибуты
•	aria-label — текстовое описание элемента.
•	aria-labelledby — указывает элемент, который служит заголовком.
•	aria-hidden="true" — скрывает элемент от экранных дикторов.
•	role="alert" — указывает, что это важное уведомление.
Пример использования
<div role="alert">Ошибка: Неверный логин или пароль.</div>
🔹 Используется для отображения ошибок и уведомлений.
🔹 Диктор прочтет этот текст сразу после появления.
3. Как правильно использовать теги для лучшей доступности?
Некоторые HTML-теги уже семантически корректны, и их не нужно заменять <div>-ами.
Пример правильной структуры
<header>
    <h1>Заголовок страницы</h1>
</header>
<nav>
    <ul>
        <li><a href="/">Главная</a></li>
        <li><a href="/about">О нас</a></li>
    </ul>
</nav>
<main>
    <article>
        <h2>Название статьи</h2>
        <p>Текст статьи...</p>
    </article>
</main>
<footer>
    <p>© 2025 Все права защищены</p>
</footer>
🔹 Семантические теги (header, nav, main, article, footer) улучшают доступность.
🔹 Экранные дикторы корректно читают такую структуру.
4. Как сделать сайт удобным для навигации с клавиатуры?
Некоторые пользователи не могут использовать мышь и взаимодействуют с сайтом только с клавиатуры.
🔹 Основные клавиши навигации:
•	Tab — перемещение между элементами.
•	Enter — активация ссылок и кнопок.
•	Space — прокрутка страницы.
•	Esc — закрытие модальных окон.
Пример правильного фокуса
<a href="#" tabindex="0">Эта ссылка доступна с клавиатуры</a>
🔹 Атрибут tabindex="0" позволяет элементу получать фокус при нажатии Tab.
5. Как улучшить контрастность и читаемость текста?
🔹 Цветовой контраст важен для пользователей с нарушениями зрения.
🔹 Минимальное соотношение контраста текста и фона должно быть 4.5:1.
Пример хорошего контраста
body {
    color: #333; /* Темный текст */
    background-color: #FFF; /* Белый фон */
}
🔹 Используйте инструменты проверки контраста, например, WebAIM Contrast Checker.
6. Как сделать изображения доступными?
Каждое изображение должно иметь атрибут alt, чтобы его мог прочитать экранный диктор.
Пример кода
<img src="cat.jpg" alt="Черный кот на фоне окна">
🔹 Если изображение декоративное, используйте alt="", чтобы экранный диктор его игнорировал.
4. Сравнительная таблица HTML, XHTML и XML
Характеристика	HTML	XHTML	XML
Основное назначение	Отображение контента в браузере	Отображение контента в браузере с жестким синтаксисом	Хранение и передача данных
Требуется ли закрывать теги?	Нет	Да	Да
Чувствителен ли к регистру?	Нет	Да (атрибуты в нижнем регистре)	Да
Гибкость	Гибкий	Строгий	Очень строгий
Используется в	Веб-страницах	Веб-страницах (в старых системах)	API, базы данных, конфигурационные файлы

Таблица HTML-тегов с указанием типа (одиночный/парный)
Тег	Описание и назначение	Категория	Тип тега
<!DOCTYPE>	Объявляет тип документа и версию HTML.	Базовый	Одиночный
<html>	Корневой элемент HTML-документа.	Базовый	Парный
<head>	Содержит метаинформацию (заголовок, ссылки на стили, скрипты).	Метаданные	Парный
<title>	Заголовок документа (отображается во вкладке браузера).	Метаданные	Парный
<meta>	Метаданные документа (кодировка, описание, ключевые слова).	Метаданные	Одиночный
<link>	Подключает внешние ресурсы (например, CSS-файлы).	Метаданные	Одиночный
<style>	Встроенные CSS-стили.	Стили	Парный
<script>	Подключает или встраивает JavaScript-код.	Скрипты	Парный¹
<body>	Содержит видимое содержимое страницы.	Базовый	Парный
<h1>-<h6>	Заголовки разного уровня (h1 — самый важный).	Текст	Парный
<p>	Параграф текста.	Текст	Парный
<a>	Гиперссылка. Атрибут href задаёт URL.	Ссылки	Парный
<img>	Вставляет изображение. Атрибуты: src (путь), alt (альтернативный текст).	Медиа	Одиночный
<div>	Блочный контейнер для стилизации или группировки элементов.	Структура	Парный
<span>	Строчный контейнер для стилизации фрагментов текста.	Текст	Парный
<ul>, <ol>, <li>	Создают списки (маркированный, нумерованный, элементы списка).	Списки	Парные
<table>, <tr>, <td>, <th>	Таблицы (основной тег, строки, ячейки, заголовочные ячейки).	Таблицы	Парные
<form>	Форма для ввода данных пользователем.	Формы	Парный
<input>	Поле ввода (текст, пароль, чекбокс и т.д.). Тип задаётся атрибутом type.	Формы	Одиночный
<button>	Кликабельная кнопка.	Формы	Парный
<textarea>	Многострочное текстовое поле.	Формы	Парный
<select>, <option>	Выпадающий список и его элементы.	Формы	Парные
<label>	Подпись для элемента формы (улучшает доступность).	Формы	Парный
<header>	Шапка сайта или раздела (HTML5).	Семантика	Парный
<footer>	Подвал сайта или раздела (HTML5).	Семантика	Парный
<nav>	Навигационное меню (HTML5).	Семантика	Парный
<section>	Секция документа (HTML5).	Семантика	Парный
<article>	Независимый контент (статья, пост) (HTML5).	Семантика	Парный
<aside>	Боковая панель или дополнительный контент (HTML5).	Семантика	Парный
<main>	Основное содержимое страницы (HTML5).	Семантика	Парный
<figure>, <figcaption>	Группирует медиаконтент с подписью (HTML5).	Медиа	Парные
<video>, <audio>	Встраивает видео или аудио (HTML5). Атрибут controls добавляет элементы управления.	Медиа	Парные
<iframe>	Встраивает внешнюю веб-страницу или контент.	Медиа	Парный
<br>	Перенос строки.	Текст	Одиночный
<hr>	Горизонтальная линия.	Текст	Одиночный
<strong>	Выделяет важный текст (жирный).	Текст	Парный
<em>	Выделяет текст курсивом (акцентирование).	Текст	Парный
<code>	Отображает текст как код.	Текст	Парный
<pre>	Сохраняет форматирование текста (пробелы, переносы).	Текст	Парный
<mark>	Выделяет текст цветом (HTML5).	Текст	Парный
<time>	Указывает дату/время (HTML5).	Семантика	Парный
<progress>	Индикатор прогресса (HTML5).	Формы	Парный
<canvas>	Холст для рисования графики через JavaScript (HTML5).	Медиа	Парный
<svg>	Встраивает векторную графику (SVG).	Медиа	Парный
<datalist>	Список вариантов для поля ввода (HTML5).	Формы	Парный
<details>, <summary>	Раскрывающийся блок с заголовком (HTML5).	Интерактив	Парные
<template>	Шаблон для клонирования в JavaScript (HTML5).	Скрипты	Парный





















Команды Git
Команда	Описание	Категория
git init	Инициализирует новый локальный репозиторий.	Настройка
git clone <url>	Клонирует удалённый репозиторий в текущую директорию.	Работа с удалёнными репами
git add <file>	Добавляет изменения в файле в индекс (staging area).	Основные команды
git commit -m "сообщение"	Фиксирует изменения в индексе с комментарием.	Основные команды
git status	Показывает состояние рабочих файлов и индекса.	Информация
git push	Отправляет коммиты в удалённый репозиторий.	Удалённые репозитории
git pull	Забирает изменения из удалённого репозитория и сливает с текущей веткой.	Удалённые репозитории
git branch	Показывает список веток. -d <ветка> удаляет ветку.	Ветвление
git checkout <ветка>	Переключается на указанную ветку. -b создаёт новую ветку.	Ветвление
git merge <ветка>	Сливает указанную ветку с текущей.	Ветвление
git log	Показывает историю коммитов. --oneline для краткого вывода.	История
git diff	Показывает изменения между рабочими файлами и индексированными версиями.	Изменения
git reset <файл>	Убирает файл из индекса (оставляет изменения в рабочей директории).	Отмена изменений
git reset --hard HEAD	Отменяет все незакоммиченные изменения (осторожно!).	Отмена изменений
git revert <commit>	Создаёт новый коммит, отменяющий изменения указанного коммита.	Отмена изменений
git stash	Временно сохраняет незакоммиченные изменения. pop восстанавливает их.	Временное сохранение
git remote add <имя> <url>	Добавляет удалённый репозиторий под указанным именем (например, origin).	Удалённые репозитории
git fetch	Загружает изменения из удалённого репозитория, но не сливает их.	Удалённые репозитории
git rebase <ветка>	Перебазирует текущую ветку на указанную (альтернатива merge).	Ветвление
git tag <имя-тега>	Создаёт тег для текущего коммита. -a для аннотированного тега.	Теги
git rm <файл>	Удаляет файл из рабочей директории и индекса.	Управление файлами

