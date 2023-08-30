### Пример функции

```src/sum.ts```
```typescript
export function sum(x: number, y: number): number {
    return x + y
}
```

---

### Тест (спецификация) функции

```src/sum.spec.ts```
```typescript
import { sum } from "./sum"

test("Сумма", () => {
    expect(sum(2, 2)).toBe(4)
    expect(sum(2, 3)).toBe(4)
})
```

---

### Запуск теста

```
jest                 
    ...
    ● Сумма
    expect(received).toBe(expected) // Object.is equality
    Expected: 4
    Received: 5
      3 | test("Сумма", () => {
      4 |     expect(sum(2, 2)).toBe(4)
    > 5 |     expect(sum(2, 3)).toBe(4)
        |                       ^
      6 | })
    ...
```

---

### Запуск теста

```
jest
 PASS  src/sum.spec.ts
  √ Сумма (2 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.306 s, estimated 2 s
Ran all test suites.
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какие основные типы переменных в TS и JS?",    
    "answers": [
        { "isRight":true, "text":"<code>number, string, boolean</code>"},
        { "isRight":false, "text":"<code>number, int, float</code>"},
        { "isRight":false, "text":"<code>number, char, array</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Как правильно записывается проверка в тесте?",    
    "answers": [
        { "isRight":true, "text":"<code>expect(вычисляемое значение).toBe(ожидаемое значение)</code>"},
        { "isRight":false, "text":"<code>expect(ожидаемое значение).toBe(вычисляемое значение)</code>"},
        { "isRight":false, "text":"<code>test(вычисляемое значение).expext(ожидаемое значение)</code>"}
    ]
}'></div>

----

### Панель отладки

![](panel_debug.jpg)

---

### Точка останова

![](breakpoint.jpg)

---

### Запуск отладки

![](run_debug.jpg)

---

### Состояние программы

![](debug_state.jpg)

---

### Стек вызовов

![](debug_stack.jpg)

---

<div class='quiz' data-quiz='{ 
    "question": "Как можно добавить точку останова?",    
    "answers": [
        { "isRight":true, "text":"Кликнув по полю в строке исходного кода"},
        { "isRight":true, "text":"Во вкладке \"Точки останова\" панели \"Запуск и отладка\""},
        { "isRight":false, "text":"В терминале отладки javascript"},
        { "isRight":false, "text":"В файле <code>jest.config.js</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие горячие главишы используются для продолжения выполнения программы, выполнения шага с обходом и шага с обходом?",    
    "answers": [
        { "isRight":true, "text":"F5, F10, F11"},
        { "isRight":false, "text":"F5, F9, F10"},
        { "isRight":false, "text":"F6, F9, F10"}
    ]
}'></div>

----

### Отладка в браузере

```src/index.ts```
```typescript
import { sum } from "./sum"

console.log(sum(2, 2))
```

```
npm run start
```

---

### Отладчик браузера. Исходники

![](debug_browser.jpg)

---

### Отладчик браузера. Состояние

![](debug_browser.jpg)


---

<div class='quiz' data-quiz='{ 
    "question": "Как запустить отладку в браузере?",    
    "answers": [
        { "isRight":true, "text":"<code>npm run start</code>"},
        { "isRight":false, "text":"<code>npm run jest</code>"},
        { "isRight":false, "text":"<code>jest</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "На какой странице можно найти исходные коды в отладчике браузера?",    
    "answers": [
        { "isRight":true, "text":"top-webpack-src"},
        { "isRight":false, "text":"top-localhost"},
        { "isRight":false, "text":"top-webpack-webpack"}
    ]
}'></div>