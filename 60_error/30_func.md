### Чистые функции

- детерминированные
- без побочных эффектов

---

### Побочный эффект исключений

---

### Чистый результат с ошибками

```typescript
type Result<T, E> = 
    Ok<T, E>    // contains a success value of type T
    | Err<T, E> // contains a failure value of type E
```

----

### Безопасный парсинг

```typescript
enum JsonErrorReason { Parse, Type }
class JsonError {
    constructor(
        public reason: JsonErrorReason
    ) { }
}
function safeParse<T>(
    str: string,
    guard: (obj: any) => obj is T
): Result<T, JsonError> {
```

---

### Безопасный парсинг

```typescript
function safeParse<T>(
    str: string,
    guard: (obj: any) => obj is T
): Result<T, JsonError> {
    let obj
    try { 
        obj = JSON.parse(str)
    } catch (e) {
        return err(new JsonError(JsonErrorReason.Parse))
    }
    if (guard(obj)) return ok(obj)
    else return err(new JsonError(JsonErrorReason.Type))
}
```

---

### Защита типа класса

```typescript
class Student {
    constructor(public name: string) { }
}
function studentGuard(obj: any): obj is Student {
    const keys = Object.keys(obj)
    if (keys.length != 1) return false
    if (keys[0] !== "name") return false
    return true
}
```

---

### Работа безопасного парсинга

```typescript
console.log(safeParse(`{"name"}`, studentGuard))
console.log(safeParse(`{"name":"Ivan", "a": 1}`, studentGuard))
console.log(safeParse(`{"names":"Ivan"}`, studentGuard))
console.log(safeParse(`{"name":"Ivan"}`, studentGuard))
```
```
Err { error: JsonError { reason: 0 } }
Err { error: JsonError { reason: 1 } }
Err { error: JsonError { reason: 1 } }
Ok { value: { name: 'Ivan' } }
```

----

### Ошибки в нескольких функциях

```typescript
class MyError { }

function signStudentToLesson(
    _student: string,
    _lesson: string
): Result<Lesson, MyError> 
```

---

### Объединение функций

```typescript
function signStudentToLesson(
    _student: string,
    _lesson: string
): Result<Lesson, MyError> {
    const s = Result.combine([
        safeParse(_lesson, lessonGuard),
        safeParse(_student, studentGuard)
    ])
    if (s.isOk()) {
        const [lesson, student] = s.value
        lesson.students.push(student)
        return ok(lesson)}
    return err(new MyError())}
```

---

### Объединение функций

```typescript
console.log(signStudentToLesson(
    `{"name":"Ivan"}`, `{"name":"Math", "students": []}`))
console.log(signStudentToLesson(
    `{"names":"Ivan"}`, `{"name":"Math", "students": []}`))
console.log(signStudentToLesson(
    `{"names":"Ivan"}`, `{"name":"Math"}`))
```
```
Ok { value: { name: 'Math', students: [ [Object] ] } }
Err { error: MyError {} }
Err { error: MyError {} }
```

----

### Result и Promise

```typescript
function getSite(url: string): ResultAsync<Response, Error> {
    return ResultAsync.fromPromise(
        fetch(url),
        (e) => {
            console.log(e)
            return new Error()
        }
    )
}
```

---

### Result и Promise

```typescript
const urls = ["http://ya.ru", "http://aa.aa"]
urls.forEach(value => {
    getSite(value).andThen(
        t => {
            console.log(t.status)
            return ok(t)
        }
    )
})
```
```
TypeError: fetch failed
    ...
200
```

---

### Result и throw

```typescript
const safeJsonParse =
    Result.fromThrowable(
        JSON.parse,
        e => console.log("Parse Error")
    )
safeJsonParse(`{"name"}`)
```
```
Parse Error
```
