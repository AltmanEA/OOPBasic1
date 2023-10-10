### Типы в JS

```typescript
const num = 3
const fun = function () { }
const obj1 = { "x": 1 }
const obj2 = { hello() { return "Hello" } }
console.log(typeof num)
console.log(typeof fun)
console.log(typeof obj1)
console.log(typeof obj2)
```
```typescript
number
function
object
object
```

---

### Типы в TS

```typescript
const num = 3
const fun = function () { }
const obj1 = { "x": 1 }
const obj2 = { hello() { return "Hello" } }

type Num = typeof num   // type Num = 3
type Fun = typeof fun   // type Fun = () => void
type Obj1 = typeof obj1 // type Obj1 = {
                        //      x: number;
                        // }
type Obj2 = typeof obj2 // type Obj2 = {
                        //      hello(): string;
                        // }
```

---

<div class='quiz' data-quiz='{ 
    "question": "В каких случаях <code>typeof</code> вызывается во время компиляции?",    
    "answers": [
        { "isRight":true, "text":"<code>type Num = typeof num </code>"},
        { "isRight":true, "text":"<code>function a(): typeof x</code>"},
        { "isRight":false, "text":"<code>console.log(typeof num)</code>"},
        { "isRight":false, "text":"<code>if (typeof x === \"number\")</code>"}
    ]
}'></div>


----

### Type guard в JS

```javascript
function sum(x) {
    if (typeof x === "number")
        return x
    if (Array.isArray(x)) { // only number?
        result = 0
        for (i of x)
            result += i
        return result
    }         
    throw Error
}
```

---

### Type guard в TS

```javascript
function sum(x: number | number[]): number{
    if(typeof x ==="number")
        return x
    else    {
        let result = 0
        for(let i of x)
            result += i
        return result
    }        
}

console.log(sum(1))
console.log(sum([1,2]))
console.log(sum("a"))
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какого типа вернет результат функция <code>function len(x: number | string) { if(typeof x ===\"number\") return String(x).length else return x.length }</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>number</code>"},
        { "isRight":false, "text":"<code>string</code>"},
        { "isRight":false, "text":"<code>string[]</code>"},
        { "isRight":false, "text":"<code>number[]</code>"}
    ]
}'></div>

----

### User defined type guard

```javascript
type Index = number

function isIndex(x: number): x is Index {
    if (x % 1 !== 0) return false
    if (x < 0) return false
    if (x > 8) return false
    return true
}
```

---

### User defined type guard

```javascript
function getChar(board: string, index: number): string {
    if(isIndex(index))
        return board[index]
    else
        throw Error
}

console.log(getChar("123456789", 1))
console.log(getChar("123456789", 10))
```
```
2

C:\work\project\dist\index.js:15
        throw Error;
        ^
[Function: Error] { stackTraceLimit: 10 }
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какого фактически тип возвращает функция <code>function isIndex(x: number): x is Index</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>boolean</code>"},
        { "isRight":false, "text":"<code>string</code>"},
        { "isRight":false, "text":"<code>object</code>"},
        { "isRight":false, "text":"<code>number</code>"}
    ]
}'></div>

----

### Option type

```javascript
function inc(x: number, y?: number){
    console.log(typeof y)
    return x + (y ?? 1)
}

console.log(inc(10))
console.log(inc(20, 2))
// console.log(inc(30, null))
```
```
undefined
11
number
22
```

---

### Null type

```javascript
function inc(x: number, y: number | null){
    console.log(typeof y)
    return x + (y ?? 1)
}

// console.log(inc(10))
console.log(inc(20, 2))
console.log(inc(30, null))
```
```
number
22
object
31
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какого типа параметр у функции <code>function a(x?: string)</code>",    
    "answers": [
        { "isRight":true, "text":"<code>string | undefined</code>"},
        { "isRight":false, "text":"<code>string | null</code>"},
        { "isRight":false, "text":"<code>string</code>"},
        { "isRight":false, "text":"<code>null</code>"}
    ]
}'></div>