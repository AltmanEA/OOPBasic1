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