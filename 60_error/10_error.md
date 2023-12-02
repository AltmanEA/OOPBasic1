### Проблема обработки ошибок

```typescript
function sumInt(a: string, b: string): number | null {
    const an = Number(a)
    if (Number.isNaN(an)) return null
    if (an % 1 !== 0) return null
    const bn = Number(b)
    if (Number.isNaN(an)) return null
    if (bn % 1 !== 0) return null
    return an + bn
}
console.log(sumInt("1", "1"))
console.log(sumInt("1.1", "1"))
console.log(sumInt("a", "b"))
```

---

### Блок try

```typescript
function sumInt(a: string, b: string): number | null {
    try {
        return Number(BigInt(a) + BigInt(b))
    } catch (e) {
        return null
    }
}
console.log(sumInt("1", "1"))
console.log(sumInt("1.1", "1"))
console.log(sumInt("a", "b"))
```

---

### Проброс ошибок

```typescript
function sumInt(a: string, b: string): number  {
        return Number(BigInt(a) + BigInt(b))
}
function longEval(a: string, b: string): number | null {
    try {
        return sumInt(a, b)
    } catch (e){
        return null
    }
}
console.log(longEval("1", "1"))
console.log(longEval("0.1", "1"))
console.log(longEval("a", "b"))
```

----

### Объекты-ошибки

```typescript
function longEval(a: string, b: string): number | null {
    try {
        return sumInt(a, b)
    } catch (e){        
        console.log((e as Error).message)
        return null } }
console.log(longEval("1", "1"))
console.log(longEval("0.1", "1"))
console.log(longEval("a", "b"))
```
```
2
Cannot convert 0.1 to a BigInt
null
Cannot convert a to a BigInt
null
```

---

### Класс Error

```typescript
    } catch (e){
        const ee: Error = e as Error
        console.log("message: ", ee.message)
        console.log("stack: ", ee.stack)
        console.log("name: ", ee.name)
        return null
    }
```
```
message:  Cannot convert a to a BigInt
stack:  SyntaxError: Cannot convert a to a BigInt
    at BigInt (<anonymous>)
    at sumInt (C:\work\project\dist\index.js:3:19)
    at longEval (C:\work\project\dist\index.js:7:16)
    at Object.<anonymous> (C:\work\project\dist\index.js:19:13)
    ...
name:  SyntaxError
```

---

### Error types

- RangeError
- ReferenceError
- SyntaxError
- TypeError
- InternalError 

----


### Создание собственных исключений

```typescript
function getDay(number: number): string {
    const days = ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"]
    if((number<0) || (number>6) )
        throw new RangeError(`Нет дня ${number}`)
    const result: string | undefined = days[number]
    if (!result) throw new Error()
    return result
}
console.log(getDay(0))
console.log(getDay(10))
```
```
Пн
C:\work\project\dist\index.js:5
        throw new RangeError("\u041D\u0435\u0442 \u0434\u043D\u044F ".concat(number));
        ^

RangeError: Нет дня 10
    at getDay (C:\work\project\dist\index.js:5:15)
```

---

### Анализ исключений

```typescript
function checkDay(number: number): string {
    try {
        return getDay(number)
    } catch (e) {
        if (e instanceof RangeError)
            return "Нет такого дня"
        else
            throw e
    }
}
console.log(checkDay(0))
console.log(checkDay(10))
console.log(checkDay(1.1))
```
```
Пн
Нет такого дня
C:\work\project\dist\index.js:19
            throw e;
            ^

Error
    at getDay (C:\work\project\dist\index.js:8:15)
```

---

### Создание класса исключений

```typescript
class NotIndexError extends Error {
    constructor(message: string) {
        super(message)
        this.name = "It is not index" } }
function getDay(number: number): string {
    const days = ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"]
    if ((number < 0) || (number > 6) || (number % 1 !==0))
        throw new NotIndexError("")
    return days[number] }
console.log(getDay(0))
console.log(getDay(10))
console.log(getDay(1.1))
```
```
Пн
C:\work\project\dist\index.js:29
        throw new NotIndexError("");
        ^

It is not index
    at new NotIndexError (C:\work\project\dist\index.js:20:28)
```

----

### Общий синтаксис

```typescript
try {
  // some code that may throw an error
} catch (error) {
  // some code that handles the error
} finally {
  // some code that will always run
}
```

---

### Недостатки

```typescript
function getDay(number: number): string {
```

---

### Контролируемые исключения

```java
public String input() throws MyException
```