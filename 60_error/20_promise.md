### Асинхронный вызов

```typescript
setTimeout(() => console.log("Async"), 1000)
console.log("Sync")
```
```
Sync
Async
```

---

### Promise

```typescript
function getSite(url: string): void {
    fetch(url).then(                        // Promise<Response>
        value => console.log(value.status), // onfulfilled
        reason => console.log(reason.cause) // onrejected
    )
}
const urls = ["http://ya.ru", "http://aa.aa"]
urls.forEach(value => getSite(value))
```
```
Error: getaddrinfo ENOTFOUND aa.aa
    at GetAddrInfoReqWrap.onlookupall [as oncomplete] (node:dns:118:26) {
  errno: -3008,
  code: 'ENOTFOUND',
  syscall: 'getaddrinfo',
  hostname: 'aa.aa'
}
200
```

---

### Async-await

```typescript
async function getSiteAsync(url: string): Promise<void> {
    let result
    try {
        result = await fetch(url)
    }
    catch (e: any){
        console.log(e.cause)    
    }
    console.log(result?.status)
}
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какие обработчики можно «навешать» на promise?",    
    "answers": [
        { "isRight":false, "text":"<code>onfinish</code>"},
        { "isRight":false, "text":"<code>onclick</code>"},
        { "isRight":true, "text":"<code>onrejected</code>"},
        { "isRight":true, "text":"<code>onfulfilled</code>"}
    ]
}'></div>


---

<div class='quiz' data-quiz='{ 
    "question": "Какой модификатор функции указывает на то, что она возвращает promise?",    
    "answers": [
        { "isRight":false, "text":"<code>promise</code>"},
        { "isRight":false, "text":"<code>public</code>"},
        { "isRight":false, "text":"<code>await</code>"},
        { "isRight":true, "text":"<code>async</code>"}
    ]
}'></div>

----

### Несколько асинхронных вызовов

```typescript
function getSiteBody(url: string): void {
    fetch(url).then(
        value => value.text()   // Promise<string>
            .then(value => console.log(value.slice(0, 30))),
        reason => console.log(reason.cause)
    )
}
```
```
Error: getaddrinfo ENOTFOUND aa.aa
    at GetAddrInfoReqWrap.onlookupall [as oncomplete] (node:dns:118:26) {
  errno: -3008,
  code: 'ENOTFOUND',
  syscall: 'getaddrinfo',
  hostname: 'aa.aa'
}
<!doctype html><html prefix="o
```

---

### Несколько асинхронных вызовов

```typescript
function getSiteChain(url: string): void {
    fetch(url)
        .then(value => value.text())
        .then(value => console.log(value.slice(0, 30)))
        .catch(r => console.log("Error"))
}
```
```
Error
<!doctype html><html prefix="o
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какие методы есть у promise?",    
    "answers": [
        { "isRight":false, "text":"<code>finally</code>"},
        { "isRight":false, "text":"<code>try</code>"},
        { "isRight":true, "text":"<code>catch</code>"},
        { "isRight":true, "text":"<code>then</code>"}
    ]
}'></div>

----

### Параллельное исполнение

```typescript
Promise.all(urls.map(url => fetch(url)))
    .then(values => values.forEach(
        value => console.log(value.status)        
    ))
    .catch(r => console.log("Error"))
```
```
Error
```

---

### Параллельное исполнение

```typescript
Promise.race(urls.map(url => fetch(url)))
    .then(value => console.log(value.status))
    .catch(r => console.log("Error"))    
```
```
Error
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какой метод класса <code>Promise</code> возвращает promise c массивом результатов других promise?",    
    "answers": [
        { "isRight":false, "text":"<code>map</code>"},
        { "isRight":false, "text":"<code>array</code>"},
        { "isRight":false, "text":"<code>race</code>"},
        { "isRight":true, "text":"<code>all</code>"}
    ]
}'></div>


---

<div class='quiz' data-quiz='{ 
    "question": "Какой метод класса <code>Promise</code> возвращает первый завершившийся promise?",    
    "answers": [
        { "isRight":false, "text":"<code>map</code>"},
        { "isRight":false, "text":"<code>array</code>"},
        { "isRight":true, "text":"<code>race</code>"},
        { "isRight":false, "text":"<code>all</code>"}
    ]
}'></div>