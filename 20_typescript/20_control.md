### Ветвление

```typescript
let a, b = 3
if (b % 2)
    a = "Нечетное"
else
    a = "Четное"
console.log(a)
```
```typescript
Нечетное
```

---

### Вложенные ветвлений

```typescript
function isLeapYear(year: number): boolean {
    if (year % 4 != 0) {
        return false
    } else if (year % 100 == 0 && year % 400 != 0) {
        return false
    } else {
        return true
    }
}
let year = 2000
console.log("Is ", year, "a leap year ?", isLeapYear(year))
...
```
```typescript
Is  2000 a leap year ? true
Is  2024 a leap year ? true
Is  2100 a leap year ? false
```

---

### Оператор ветвления

```typescript
const b = 3
const a = b % 2 ? "Нечетное" : "Четное"
```
```typescript
Нечетное
```

---

### Конструкция выбора

```typescript
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

---

<div class='quiz' data-quiz='{ 
    "question": "Что нужно вставить вместо многоточия в код <code>(year % 4 != 0) ? false : ... </code> для правильного определения високосного года?",    
    "answers": [
        { "isRight":true, "text":"<code>!(year % 100 == 0 && year % 400 != 0)</code>"},
        { "isRight":true, "text":"<code>year % 100 != 0 || year % 400 == 0</code>"},
        { "isRight":false, "text":"<code>year % 100 == 0 && year % 400 != 0</code>"},
        { "isRight":false, "text":"<code>year % 100 != 0 && year % 400 == 0</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие ключевые слова используются в JS для ветвления программы?",    
    "answers": [
        { "isRight":true, "text":"<code>if</code>"},
        { "isRight":true, "text":"<code>else</code>"},
        { "isRight":false, "text":"<code>elseif</code>"},
        { "isRight":true, "text":"<code>switch</code>"}
    ]
}'></div>

----

### Цикл итерации

```typescript
let bits = 10
while (bits > 0) {
    const tmp = Math.floor(bits / 2)
    console.log(bits - 2 * tmp)
    bits = tmp
}
```
```typescript
0
1
0
1
```
---

### Цикл итерации

```typescript
let bits = 10
do {
    const tmp = Math.floor(bits / 2)
    console.log(bits - 2 * tmp)
    bits = tmp
} while (bits > 0) 
```
```typescript
0
1
0
1
```

---

### Цикл перебора

```typescript
const a = [0, 1, 2]
for(let i=0; i<a.length; i++)
    console.log(a[i])
```
```typescript
0
1
2
```

---

### Прерывания циклов

```typescript
outer: for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Значение на координатах (${i},${j})`, '');

    // если пустая строка или Отмена, то выйти из обоих циклов
    if (!input) break outer; // (*)

    // сделать что-нибудь со значениями...
  }
}

alert('Готово!');
```

---

<div class='quiz' data-quiz='{ 
    "question": "В каком порядке идут позиции в управляющей конструкции <code>for</code>?",    
    "answers": [
        { "isRight":true, "text":"инициализация; условие_окончаний; шаг"},
        { "isRight":false, "text":"шаг; условие_окончаний; инициализация"},
        { "isRight":false, "text":"инициализация; шаг; условие_окончаний"},
        { "isRight":false, "text":"шаг; инициализация; условие_окончаний"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "При какой форме тело цикла выполниться не меньше одного раза",    
    "answers": [
        { "isRight":true, "text":"<code>do-while</code>"},
        { "isRight":false, "text":"<code>while</code>"},
        { "isRight":false, "text":"<code>for</code>"},
        { "isRight":false, "text":"<code>do-for</code>"}
    ]
}'></div>

----

### Функции

```typescript
function имя(
  параметр1: тип,
  параметр2: тип,
  ...
): тип_результата {  
    тело_функции
    ...
    return _результат_
}
```

---

### Функциональный тип

```typescript
const isOdd: (x: number) => boolean =
    function (x: number): boolean {
        return x % 2 == 1
    }
```

---

### Функции высших порядков

```typescript
function filter(
    arr: number[],
    predicate: (x: number) => boolean
): number[] {
    const result: number[] = []
    for(let i = 0; i<arr.length; i++)
        if(predicate(arr[i]))
            result.push(arr[i])
    return result
}

console.log(
    filter([0, 1, 2, 3, 4, 5], isOdd)
)
```

---

### Стрелочные функции

```typescript
const isOdd: (x: number) => boolean
    = (x: number) => x % 2 == 1

console.log(
    filter(
        [0, 1, 2, 3, 4, 5],
        (x: number) => x % 2 == 1
    )
)
```

---

<div class='quiz' data-quiz='{ 
    "question": "Перечислите особенности функций высших порядков",    
    "answers": [
        { "isRight":true, "text":"может принимать аргументы в виде функций"},
        { "isRight":true, "text":"может возвращать результат в виде функций"},
        { "isRight":false, "text":"записывается с помощью стрелочной нотации"},
        { "isRight":false, "text":"записывается с помощью ключевого слова <code>function</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какой тип у функций-предикатов?",    
    "answers": [
        { "isRight":true, "text":"<code>(x: number) => boolean</code>"},
        { "isRight":true, "text":"<code>(x: string) => boolean</code>"},
        { "isRight":false, "text":"<code>(x: number) => number</code>"},
        { "isRight":false, "text":"<code>(x: number) => string</code>"}
    ]
}'></div>
