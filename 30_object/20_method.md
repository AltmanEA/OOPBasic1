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

----

### Прототип функций

```typescript
const x = function(){}
```

<img src="fun_proto.png" width="120%"/>
