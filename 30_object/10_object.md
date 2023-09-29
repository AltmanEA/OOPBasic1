### Ссылка

<div style="display: flex;">
    <div style="flex: 2;">
<pre class="javascript"><code>const a = {
    "x": 1
}</code></pre>
    </div>
    <div style="flex: 2;">
	    <img src="ref.svg"/>
    <div>
<div>

<div class="ea_table">

---

### Копирование ссылки

<div style="display: flex;">
    <div style="flex: 2;">
<pre class="javascript"><code>const b = a
a.x = -1
console.log(a)
console.log(b)</code></pre><pre><code>{ x: -1 }
{ x: -1 }</code></pre>
    </div>
    <div style="flex: 2;">
	    <img src="copy_ref.svg"/>
    <div>
<div>

---

### Копирование объектов

<div style="display: flex;">
    <div style="flex: 2;">
<pre class="javascript"><code>const c = Object.assign({}, a)
a.x = -1
console.log(a)
console.log(c)</code></pre><pre><code>{ x: -1 }
{ x: 1 }</code></pre>
    </div>
    <div style="flex: 2;">
	    <img src="copy_obj.svg"/>
    <div>
<div>

---

### Копирование массивов

```typescript
const a: number[] = [1, 2, 3]
const b = a
const c = Object.assign({}, a)
const d = a.slice()
a[1] = -1
console.log(b)
console.log(c)
console.log(d)
```
```typescript
[ 1, -1, 3 ]
{ '0': 1, '1': 2, '2': 3 }
[ 1, 2, 3 ]
```

---

<div class='quiz' data-quiz='{ 
    "question": "Как правильно создать копию массива <code>a</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>a.slice()</code>"},
        { "isRight":true, "text":"<code>[...a]</code>"},
        { "isRight":false, "text":"<code>Object.assign({}, a)</code>"},
        { "isRight":false, "text":"<code>a</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Что из перечисленного размещается в динамической памяти",    
    "answers": [
        { "isRight":true, "text":"объекты"},
        { "isRight":true, "text":"массивы"},
        { "isRight":false, "text":"числа"},
        { "isRight":false, "text":"ссылки"}
    ]
}'></div>

----

### Вложенные объекты

<div style="display: flex;">
    <div style="flex: 2;">
<pre class="javascript"><code>const a = {
    x: { x: 1 }
}
const b = Object.assign({}, a)
a.x.x=-1
console.log(b)</code></pre><pre><code>{ x: { x: -1 } }</code></pre>
    </div>
    <div style="flex: 2;">
	    <img src="nested_object.svg"/>
    <div>
<div>

---

### Копирование вложенных объектов

```typescript
const a = {
    x: {
        x: 1
    }
}
const b = Object.assign({}, a)
const c = JSON.parse(JSON.stringify(a)) as typeof a
a.x.x=-1
console.log(b)
console.log(c)
```
```typescript
{ x: { x: -1 } }
{ x: { x: 1 } }
```

---

### Копирование вложенных массивов

```typescript
const a = [ [0, 1], [2]]
const b = [...a]
const c = JSON.parse(JSON.stringify(a)) as typeof a
const d = a.map(e => e.slice())
a[0][0] = -1
console.log(b)
console.log(c)
console.log(d)
```
```typescript
[ [ -1, 1 ], [ 2 ] ]
[ [ 0, 1 ], [ 2 ] ]
[ [ 0, 1 ], [ 2 ] ]
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какие команды выполняют глубокое копирование массива <code>a</code>?",    
    "answers": [
        { "isRight":false, "text":"<code>a.slice()</code>"},
        { "isRight":false, "text":"<code>[...a]</code>"},
        { "isRight":true, "text":"<code>JSON.parse(JSON.stringify(a)) as typeof a</code>"},
        { "isRight":true, "text":"<code>a.map(e => e.slice())</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие команды позволяет получить представление объекта <code>a</code> в виде строки?",    
    "answers": [
        { "isRight":true, "text":"<code>JSON.stringify(a)</code>"},
        { "isRight":false, "text":"<code>JSON.parse(a)</code>"},
        { "isRight":false, "text":"<code>String(a)</code>"},
        { "isRight":false, "text":"<code>a.toString()</code>"}
    ]
}'></div>

----

### Сравнение примитивных типов

```typescript
const a: any = 0
const b: any = "0"
console.log(a==b, a===b)
```
```typescript
true false
```

---

### Сравнение объектов

```typescript
const a = { x: 1}
const b = a
const c = Object.assign({}, a)
const d = { x: 1}
console.log(a==b, a===b)
console.log(a==c, a===c)
console.log(a==d, a===d)
```
```typescript
true true
false false
false false
```

---

### Структурное сравнение массивов

```typescript
function array_equals(a: any[], b: any[]): boolean {
    if (a.length != b.length) return false
    // if (typeof a[0] !== typeof b[0] ) return false
    for (let i = 0; i < a.length; i++)
        if (a[i] !== b[i])
            return false
    return true
}
```

---

### Структурное сравнение объектов (ts)

```typescript
function equals(a: object, b: object): boolean {
    if (typeof a !== typeof b) return false
    const a_key = Object.keys(a)
    if (!array_equals(a_key, Object.keys(b)))
        return false
    for (let i of a_key)
        if (a[i as keyof typeof a] !== 
			b[i as keyof typeof b])
            return false
    return false
}
```

---

### Структурное сравнение объектов (js)

```typescript
function equals(a, b) {
    if (typeof a !== typeof b)
        return false;
    var a_key = Object.keys(a);
    if (!array_equals(a_key, Object.keys(b)))
        return false;
    for (var _i = 0, a_key_1 = a_key;
        _i < a_key_1.length; _i++) {
        var i = a_key_1[_i];
        if (a[i] !== b[i])
            return false;
    }
    return false;
}
```

---

### Глубокое сравнение

```typescript
import deepEqual from "deep-equal"

const a = { x: { x: 1 } }
const b = { x: { x: 1 } }

console.log(deepEqual(a, b))
console.log(
    JSON.stringify(a) ==
    JSON.stringify(b))
```
```typescript
true
true
```

---

<div class='quiz' data-quiz='{ 
    "question": "Как можно получить список свойств объекта <code>a</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>Object.keys(a)</code>"},
        { "isRight":false, "text":"<code>Object.assign({}, a)</code>"},
        { "isRight":false, "text":"<code>[...a]</code>"},
        { "isRight":false, "text":"<code>keyof a</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Каких операторов или функций нет в JS?",    
    "answers": [
        { "isRight":true, "text":"<code>keyof</code>"},
        { "isRight":true, "text":"<code>as</code>"},
        { "isRight":false, "text":"<code>Object.keys</code>"},
        { "isRight":false, "text":"<code>typeof</code>"}
    ]
}'></div>