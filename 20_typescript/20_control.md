### Ветвление

```typescript
var a, b = 3
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

----

### Цикл итерации

```typescript
var bits = 10
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
var bits = 10
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
for(var i=0; i<a.length; i++)
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

----

### Функции

