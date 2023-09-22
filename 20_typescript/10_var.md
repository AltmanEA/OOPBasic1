### Примитивные типы js / ts

```typescript
const hello: string = "Привет, мир"

const answer: number = 42

const yes: boolean = true
```

---

### Операции с числами

- арифметические
- Math
- побитовые

---

### Строки 

```typescript
const a = `многострочный
    string`
const b = 'Строка с "кавычками"'
const c = "\"Экранирование\" \n и спецсимволы"

console.log(a, b, c)
```

```typescript
многострочный
    string Строка с "кавычками" "Экранирование"
 и спецсимволы
```

---

### Свойства и функции строк

```typescript
const a = "строка"

console.log(a.length)
console.log(a[2])
console.log(a.indexOf("о"))
console.log(a.toUpperCase())
```

```typescript
6
р
3
СТРОКА
```
---

### Функции строк

```typescript
const a = "строка"

console.log(a.slice(2, 4))
console.log(a.search("рок"))
console.log(a.replace("рок", "джаз"))
```

```typescript
ро
2
стджаза
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какие операции с числами есть в JS?",    
    "answers": [
        { "isRight":true, "text":"Отбрасывание дробной части"},
        { "isRight":true, "text":"Округление"},
        { "isRight":false, "text":"Деление на цело"},
        { "isRight":true, "text":"Нахождение остатка от деления"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие свойства у строк есть в JS?",    
    "answers": [
        { "isRight":true, "text":"<code>length</code>"},
        { "isRight":false, "text":"<code>size</code>"},
        { "isRight":false, "text":"<code>indexOf</code>"},
        { "isRight":false, "text":"<code>toUpperCase</code>"}
    ]
}'></div>

----

### Массивы js / ts

```typescript
const arr: number[] = [1, 2, 3]
const x: number[] = new Array(9)

const complex_array: string[][] = [["one"], ["one", "two"]]

console.log(complex_array[1])
```

```typescript
[ 'one', 'two' ]
```

---

### Работа с массивами

```typescript
const arr: number[] = [1]

arr.push(2, 3); console.log(arr)
arr.unshift(-1, -2); console.log(arr)
console.log(arr.pop(), arr)
console.log(arr.shift(), arr)
```

```typescript
[ 1, 2, 3 ]
[ -1, -2, 1, 2, 3 ]
3 [ -1, -2, 1, 2 ]
-1 [ -2, 1, 2 ]
```

---

### Работа с массивами

```typescript
const arr: number[] = [1, 2, 3, 4, 5]

console.log(arr.slice(2, 4))
console.log(arr.concat(arr))
console.log(arr.indexOf(3))
```

```typescript
[ 3, 4 ]
[
  1, 2, 3, 4, 5,
  1, 2, 3, 4, 5
]
2
```

---

### Кортеж 

```typescript
const tuples: [number, string, boolean] = [1, "one", true]

const [num, _, bool] = tuples

console.log(num)
console.log(bool)
```

```typescript
1
true
```

---

### Распространение массива

```typescript
const arr: number[] = [1, 2, 3, 4, 5]

const try_change = [arr.slice(3,5), arr[2], arr.slice(0,2)]
const change = [...arr.slice(3,5), arr[2], ...arr.slice(0,2)]

console.log(try_change)
console.log(change)
```

```typescript
[ [ 4, 5 ], 3, [ 1, 2 ] ]
[ 4, 5, 3, 1, 2 ]
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какого тип будет <code>a</code> после <br><code>const a = [\"x\"]</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>string[]</code>"},
        { "isRight":false, "text":"<code>string[1]</code>"},
        { "isRight":false, "text":"<code>[string]</code>"},
        { "isRight":false, "text":"<code>string</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие функции добавляют элементы в массив?",    
    "answers": [
        { "isRight":true, "text":"<code>push</code>"},
        { "isRight":true, "text":"<code>unshift</code>"},
        { "isRight":false, "text":"<code>pop</code>"},
        { "isRight":false, "text":"<code>shift</code>"}
    ]
}'></div>

----

### Неопределенные данные

```typescript
const arr: number[] = [1]

console.log(arr[1])
```

```typescript
undefined
```

---

### Операции с неопределенными данными

```typescript
const num: number[] = [1]
const str: string[] = ["1"]
const _num: number = num[1]
const _str: string = str[1]

console.log(_num + 2)
console.log(_str + "2")
```

```typescript
NaN
undefined2
```

---

### Отсутствующие данные

```typescript

console.log(document.getElementById("root"))
console.log(document.getElementById("leaf"))
```

![](null.png)

---

### Объединение типов

```typescript
const root: HTMLElement | null = document.getElementById("root")
const leaf: HTMLElement | null = document.getElementById("leaf")
```

---

### Обработка отсутствующих данных

```typescript
const root: HTMLElement | null = document.getElementById("root")
const leaf: HTMLElement | null = document.getElementById("leaf")
if(root)
    root.textContent = "Hello"
if(leaf)
    leaf.textContent = "Hello"

console.log(root?.textContent)
console.log(leaf?.textContent)

```

![](null_chain.png)

---

### Тип any в ts

```typescript
const a: any = true
const b = a.toUpperCase()
console.log(b)
```

```typescript
let b = a.toUpperCase();
          ^

TypeError: a.toUpperCase is not a function
```

---

<div class='quiz' data-quiz='{ 
    "question": "Для каких типов данных TS требуют проверки наличия значения переменной перед использованием переменной?",    
    "answers": [
        { "isRight":true, "text":"<code>null</code>"},
        { "isRight":false, "text":"<code>undefined</code>"},
        { "isRight":false, "text":"<code>any</code>"},
        { "isRight":false, "text":"<code>number</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "В каких случаях может появиться <code>undefined</code> в программе на TS?",    
    "answers": [
        { "isRight":true, "text":"При использовании переменных типа any"},
        { "isRight":true, "text":"При вызове JS функций"},
        { "isRight":false, "text":"При вызове неиницилизированной переменной"},
        { "isRight":false, "text":"При передаче функции аргумента другого типа"}
    ]
}'></div>