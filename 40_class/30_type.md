### Равенство типов

```typescript
class Student {        
    constructor(
        public name: string, 
        public place: string
        ) { } }
class Tutor {        
    constructor(
        public name: string, 
        public place: string
        ) { }    
}
const ivan: Tutor = new Student("Иван", "22з")
```
```typescript
Student { name: 'Иван', place: '22з' }
```

---

### Равенство типов

```typescript
class Student {        
    constructor(
        public name: string, 
        public place: string
        ) { } }
class Tutor {        
    constructor(
        public name: string, 
        public place: string
        ) { }
    static institute = "МГУ"    
}
const ivan: Tutor = new Student("Иван", "22з")
```
```typescript
Student { name: 'Иван', place: '22з' }
```

---

### Проблема равенства типов

```typescript
function getDeps(tutor: Tutor[]): string[]{
    return tutor.map((t)=>{
        return t.place
    })   
}
console.log(getDeps([new Student("Иван", "22з")]))
```
```typescript
[ '22з' ]
```

---

<div class='quiz' data-quiz='{ 
    "question": "Объекты имеют один тип, если",    
    "answers": [
        { "isRight":true, "text":"они одного класса"},
        { "isRight":true, "text":"у них одинаковые свойства"},
        { "isRight":false, "text":"у них одинаковые функции"},
        { "isRight":false, "text":"у них одинаковые поля"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "При определении равенства типа объектов учитываются:",    
    "answers": [
        { "isRight":true, "text":"поля"},
        { "isRight":true, "text":"функции"},
        { "isRight":false, "text":"статические свойства"},
        { "isRight":false, "text":"аргументы конструктора"}
    ]
}'></div>

----

### Обобщенные типы (Generic)

```typescript
const arr = new Array<String>("a", "b")
```

---

### Создание обобщенных классов

```typescript
class Student {constructor(
        public name: string,
        public group: string ) { } }
class Tutor { constructor(
        public name: string,
        public dep: string ) { } }
class Group<T>{ constructor( 
        public members: T[] = []
    ) { } }
// const mathDep: Group<Tutor>
const mathDep = new Group([new Tutor("Петр", "Мат")])
```

---

### Ограничения типов

```typescript
class Group<T extends { name: string } >{
    constructor( public members: T[] = [] ) { }
    findByName(name: string): T | null {
        for (let s of this.members)
            if (s.name == name)
                return s
        return null } }
const studGroup = new Group([new Student("Иван", "22з")])
const mathDep = new Group([new Tutor("Петр", "Мат")])
const ivan = studGroup.findByName("Иван")
const petr = mathDep.findByName("Петр")
console.log(ivan)
console.log(petr)
```
```typescript
Student { name: 'Иван', group: '22з' } 
Tutor { name: 'Петр', dep: 'Мат' }
```

---

### Обобщенные типы в JS

```typescript
var Group = /** @class */ (function () {
    function Group(members) {
        if (members === void 0) { members = []; }
        this.members = members; }
    Group.prototype.findByName = function (name) {
        for (var _i = 0, _a = this.members; _
            i < _a.length; _i++) {
            var s = _a[_i];
            if (s.name == name)
                return s; }
        return null; };
    return Group; }());
```

---

<div class='quiz' data-quiz='{ 
    "question": "Когда определяется тип параметра класса?",    
    "answers": [
        { "isRight":false, "text":"При написании класса"},
        { "isRight":true, "text":"При написании кода создания объекта класса"},
        { "isRight":false, "text":"При создании объекта класса"},
        { "isRight":false, "text":"При использовании объекта класса"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какой обобщенный класс записан правильно?",    
    "answers": [
        { "isRight":true, "text":"<code>class Group< T >{}</code>"},
        { "isRight":true, "text":"<code>class Group< T extends K >{}</code>"},
        { "isRight":false, "text":"<code>class < T > Group {}</code>"},
        { "isRight":false, "text":"<code>class Group{}< T ></code>"}
    ]
}'></div>

----

### Тип this 

```typescript
class Box {
  contents: string = "";
  set(value: string): this {
    this.contents = value;
    return this;
  }
}
```

---

### Привязка this 

```typescript
class MyClass {
    name = "MyClass"
    getName(this: MyClass): string {
        return this.name
    }
}
const c = new MyClass()
c.getName()

const g = c.getName
// console.log(g())
// Контекст this типа "void" не может быть
// назначен методу this типа "MyClass".
```

---

### Переменные типа класс

```typescript
const someClass = class <Type> {
    content: Type
    constructor(value: Type) {
        this.content = value
    }
}
// const m: someClass<string>
const m = new someClass("Hello, world")
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какого типа указатель this в методах класса?",    
    "answers": [
        { "isRight":false, "text":"Тип совпадает с типом класса"},
        { "isRight":true, "text":"Тип совпадает с типом объекта"},
        { "isRight":false, "text":"<code>any</code>"},
        { "isRight":false, "text":"Тип совпадает с типом прототипа класса"}
    ]
}'></div>
