### Функции и методы

<div style="display: flex;">
    <div style="flex: 2;">
<pre class="javascript"><code>function inc(
    a: typeof x
): typeof x {
    a.x += 1
    return a
}
inc(x)
console.log(x)}</code></pre>
<pre class="javascript"><code>{ x: 2 }</code></pre>
    </div>
    <div style="flex: 2;">
<pre class="javascript"><code>const y = {
    "x": 1,
    "inc": function () {
        this.x += 1
    }
}
y.inc()
console.log(y)</code></pre>
<pre class="javascript"><code>{ x: 2, inc: [Function: inc] }</code></pre>
    <div>
<div>

---

### Указатель ```this```

<img src="this.png" width="120%"/>

---

### Потеря ```this```

<img src="this_lost.png" width="120%"/>

---

### ```this``` и стрелочные функции

```typescript
const y = {
    "x": 1,
    "inc": () => {
        this.x += 1
    }
}
```

TS7041: The containing arrow function captures the global value of 'this'.

---

<div class='quiz' data-quiz='{ 
    "question": "Что из перечисленного находится в локальных переменных функции?",    
    "answers": [
        { "isRight":true, "text":"<code>this</code>"},
        { "isRight":true, "text":"параметры"},
        { "isRight":true, "text":"переменные, объявленные внутри функции"},
        { "isRight":false, "text":"внешние переменные для функции"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Что из перечисленного находится в замыкании переменных функции?",    
    "answers": [
        { "isRight":false, "text":"<code>this</code>"},
        { "isRight":false, "text":"параметры"},
        { "isRight":false, "text":"переменные, объявленные внутри функции"},
        { "isRight":true, "text":"внешние переменные для функции"}
    ]
}'></div>

----

### Прототип объекта

```typescript
const x = {"x":1}
```
<img src="object_proto.png" width="120%"/>

---

### Прототип массива

```typescript
const z = [1]
```

<img src="array_proto.png" width="120%"/>

---

### Встроенные прототипы

![](native-prototypes-classes.svg)

---

### Прототипы примитивов

- String.prototype
- Number.prototype
- Boolean.prototype

---

<div class='quiz' data-quiz='{ 
    "question": "Каких функций нет в прототипе <code>Object</code>?",    
    "answers": [
        { "isRight":false, "text":"<code>constructor</code>"},
        { "isRight":false, "text":"<code>toString</code>"},
        { "isRight":true, "text":"<code>filter</code>"},
        { "isRight":true, "text":"<code>fill</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "При выполнение каких инструкций создается объект-обертка?",    
    "answers": [
        { "isRight":false, "text":"<code>a.toLowerCase()</code>"},
        { "isRight":true, "text":"<code>2+2</code>"},
        { "isRight":true, "text":"<code>a[2]</code>"},
        { "isRight":false, "text":"<code>a.substring(2, 4)</code>"}
    ]
}'></div>

----

### Прототип функций

```typescript
const x = function(){}
```

<img src="fun_proto.png" width="120%"/>

---

### Прототип функций

<img src="fun_proto2.jpg" width="120%"/>

---

### Привязка к объекту

```typescript
const a = {
    "x": 0,
    inc(step: number){
        this.x += step
        return this.x
    }
}
const b = {"x": 10}

const inc = a.inc
const inc_b = inc.bind(b)
console.log(inc_b(3))
```
```typescript
13
```

---

### Вызов функции с привязкой

```typescript
const a = {
    "x": 0,
    inc(step: number){
        this.x += step
        return this.x
    }
}
const b = {"x": 10}

const inc = a.inc
const inc_b = inc.bind(b)
console.log(inc_b(3))
console.log(inc.apply(b, [5]))
console.log(inc.call(b, 7))
```
```typescript
13
18
25
```

---

<div class='quiz' data-quiz='{ 
    "question": "Каких функций нет в прототипе <code>Array</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>find</code>"},
        { "isRight":false, "text":"<code>apply</code>"},
        { "isRight":false, "text":"<code>call</code>"},
        { "isRight":false, "text":"<code>bind</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Как правильно вызвать функцию <code>inc</code> для объекта <code>b</code> и передать ей аргумент <code>1</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>inc.apply(b, [1])</code>"},
        { "isRight":true, "text":"<code>inc.call(b, 1)</code>"},
        { "isRight":true, "text":"<code>inc.bind(b)(3)</code>"},
        { "isRight":false, "text":"<code>inc(b, 3)</code>"}
    ]
}'></div>
