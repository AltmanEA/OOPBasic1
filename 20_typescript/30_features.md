### Контекст

![](stack.png)

---

### Замыкание

```typescript
function filterOdd(): number[] {
    const result: number[] = []
    let elem = 0
    function isOdd(): boolean {
        return elem % 2 == 1
    }
    for (var i = 0; i < source.length; i++) {
        elem = source[i]
        if (isOdd()) { result.push(elem) }
    }
    return result
}
const source = [0, 1, 2, 3, 4, 5]
console.log(filterOdd())
```

---

### Замыкание

![](closure.png)

---

### Свойства функции

```typescript
function counter(): () => number {
    let c = 0
    return function (): number{
        return ++c
    }
}

const cnt = counter()
console.log(cnt(), cnt(), cnt())
```

```typescript
1 2 3
```

---

<div class='quiz' data-quiz='{ 
    "question": "Каким образом возвращается результат функции?",    
    "answers": [
        { "isRight":true, "text":"через стек"},
        { "isRight":false, "text":"через замыкание"},
        { "isRight":false, "text":"через глобальную переменную"},
        { "isRight":false, "text":"записывает результат по переданной ссылке"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "В замыкании функции хранится",    
    "answers": [
        { "isRight":true, "text":"внешние переменные"},
        { "isRight":false, "text":"внутренни переменные"},
        { "isRight":false, "text":"аргументы"},
        { "isRight":false, "text":"результат функции"}
    ]
}'></div>


----

### Взаимодействие с HTML

```HTML
<div id="info"></div>
```
```typescript
const info = 
    <HTMLDivElement>document
        .getElementById("info")
...
info.textContent = "Ничья"
```

---

### Свойство onClick

```typescript
    /**
     * Fires when the user clicks the left mouse button on the object
     * @param ev The mouse event.
     *
     * [MDN Reference](https://developer.mozilla.org/docs/Web/API/Element/click_event)
     */
onclick: (
    (this: GlobalEventHandlers, 
    ev: MouseEvent) => any
) | null;
```

---

### Свойства HTML элементов


```typescript
let b = 
    <HTMLButtonElement>document
        .getElementById("f" + i)
b.onclick = function (): void { step(i) }
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какого типа будет <code>info</code> после <br><code>let info = <HTMLDivElement>document.getElementById(\"info\")</code>?",    
    "answers": [
        { "isRight":true, "text":"<code>HTMLDivElement</code>"},
        { "isRight":false, "text":"<code>HTMLDivElement?</code>"},
        { "isRight":false, "text":"<code>HTMLDivElement | null</code>"},
        { "isRight":false, "text":"<code>HTMLDivElement | undefined</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "В какое свойство <code>HTMLDivElement</code> нужно записать строку, чтобы она отобразилась в браузере?",    
    "answers": [
        { "isRight":true, "text":"<code>textContent </code>"},
        { "isRight":false, "text":"<code>value</code>"},
        { "isRight":false, "text":"<code>onClick</code>"},
        { "isRight":false, "text":"<code>print</code>"}
    ]
}'></div>
