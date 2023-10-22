### Закрытые свойства

```typescript
class Count{
    private num = 0
    inc(): number{
        return this.num++
    }
}
const count = new Count()
console.log(count.inc())
console.log(count.inc())
// console.log(count.num) 
// Свойство "num" является закрытым 
//  и доступно только в классе "Count".
```
```typescript
0
1
```

---

### Закрытые свойства других объектов

```typescript
class Count{
    private num = 0
    inc(): number{
        return this.num++
    }
    add(other: Count): number{
        this.num += other.num
        return this.num
    }
}
const count = new Count()
console.log(count.inc())
console.log(count.inc())
console.log(count.add(count))
```
```typescript
0
1
4
```

---

### Модификаторы видимости

- public
- protected
- private


---

<div class='quiz' data-quiz='{ 
    "question": "Какой модификатор доступа не используется в TS?",    
    "answers": [
        { "isRight":true, "text":"internal"},
        { "isRight":false, "text":"private"},
        { "isRight":false, "text":"public"},
        { "isRight":false, "text":"protected"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "К чему может применятся модификатор private?",    
    "answers": [
        { "isRight":true, "text":"к полю"},
        { "isRight":true, "text":"к методу"},
        { "isRight":false, "text":"к локальной переменной метода"},
        { "isRight":false, "text":"к параметру метода"}
    ]
}'></div>

----

### Методы доступа к полям класса

```typescript
class Index {
    private _index: number = 0
    get index(): number {
        return this._index }
    set index(ind: number) {
        if (ind % 1 == 0 && ind > -1 && ind < 9)
            this._index = ind } }
const index =  new Index()
index.index = -1; console.log(index.index)
index.index = 1; console.log(index.index)
index.index = 1.5; console.log(index.index)
index.index = 10; console.log(index.index)
```
```typescript
0
1
1
1
```

---

### Ленивые свойства и одиночка

```typescript
class LazyLoad {
    private longLoad: string | null= null
    get load(): string{
        if(this.longLoad === null){
            this.longLoad = longLoad()
        }
        return this.longLoad
    }
}
```

---

### Реактивные свойства

```typescript
class ReactiveProps {
    private _reactive = 0
    private listeners: Array<(value: number)=>void> = []

    set reactive(value: number)  {
        this._reactive = value
        this.listeners.map(
            (f)=>{f(value)}
        )
    }   
}
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какие методы доступа записаны правильно?",    
    "answers": [
        { "isRight":true, "text":"<code>get index(): number {return this._index }</code>"},
        { "isRight":false, "text":"<code>get index(ind: number): number {this._index = ind}</code>"},
        { "isRight":false, "text":"<code>get index(ind: number): void {this._index = ind}</code>"},
        { "isRight":false, "text":"<code>get index(): void {return this._index}</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие методы доступа записаны правильно?",    
    "answers": [
        { "isRight":false, "text":"<code>set index(): number {return this._index }</code>"},
        { "isRight":false, "text":"<code>set index(ind: number): number {this._index = ind}</code>"},
        { "isRight":true, "text":"<code>set index(ind: number): void {this._index = ind}</code>"},
        { "isRight":false, "text":"<code>set index(): void {return this._index}</code>"}
    ]
}'></div>


----

### Закрытые свойства в JS

```typescript
class Count{
    private num = 0
    inc(): number{
        return this.num++
    }
}
const count: any = new Count()
console.log(count.inc())
console.log(count.inc())
console.log(count.num)
```
```typescript
0
1
2
```

---

### readonly JS

```typescript
var Student = /** @class */ (function () {
    function Student(first_name, last_name) {
        this.first_name = first_name;
        this.last_name = last_name;
    }
    return Student;
}());
```

---

### Геттеры и сеттеры в JS

```typescript
    Object.defineProperty(Index.prototype, "index", {
        get: function () {
            return this._index;
        },
        set: function (ind) {
            if (ind % 1 == 0 && ind > -1 && ind < 9)
                this._index = ind;
        },
        enumerable: false,
        configurable: true
    });
```

---

<div class='quiz' data-quiz='{ 
    "question": "Что из перечисленных возможностей TS работает в JS?",    
    "answers": [
        { "isRight":true, "text":"геттер"},
        { "isRight":true, "text":"сеттер"},
        { "isRight":false, "text":"модификатор <code>public</code>"},
        { "isRight":false, "text":"модификатор <code>readonly</code>"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какой тип используется, чтобы отключить контроль типов TS?",    
    "answers": [
        { "isRight":true, "text":"<code>any</code>"},
        { "isRight":false, "text":"<code>void</code>"},
        { "isRight":false, "text":"<code>null</code>"},
        { "isRight":false, "text":"<code>undefined</code>"}
    ]
}'></div>