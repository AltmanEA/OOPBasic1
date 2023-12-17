### Композиция

```typescript
class Person {
    constructor( public name: string ) { }
    public toString = (): string => {
        return `${this.name}`; } }
class Student {
    person: Person
    constructor( name: string,
        public group: string
    ) { this.person = new Person(name) }
    public toString = (): string => {
        return `${this.person}, гр. ${this.group}` } }
const ivan = new Student("Иван", "22з")
console.log(`${ivan}`)
```
```typescript
Иван, гр. 22з 
```

---

### Обозначение

![](composition.svg)

---

### Ассоциация и агрегация

![](aggregation.svg)

---

### Реализация ассоциации

```typescript
class Person {
    students: Student[] = []
```

---

### Плюсы и минусы композиции

```typescript
// const ivan: Person = new Student("Иван", "22з")
// В типе "Student" отсутствуют следующие свойства 
//  из типа "Person": students, name ts(2739)
```

---

<div class='quiz' data-quiz='{ 
    "question": "При реализации какого отношения в одном классе создается ссылка на другой класс?",    
    "answers": [
        { "isRight":true, "text":"композиция"},
        { "isRight":false, "text":"наследование"},
        { "isRight":true, "text":"агрегация"},
        { "isRight":false, "text":"обобщение"}
    ]
}'></div>


---

<div class='quiz' data-quiz='{ 
    "question": "При каком типе ассоциации время жизни связанных объектов может не совпадать?",    
    "answers": [
        { "isRight":false, "text":"композиция"},
        { "isRight":false, "text":"наследование"},
        { "isRight":true, "text":"агрегация"},
        { "isRight":false, "text":"обобщение"}
    ]
}'></div>

----

### Обобщение

![](template.svg)

---

### Плюсы и минусы обобщения

---

<div class='quiz' data-quiz='{ 
    "question": "В каком виде связи классов используются параметры типа?",    
    "answers": [
        { "isRight":false, "text":"композиция"},
        { "isRight":false, "text":"наследование"},
        { "isRight":false, "text":"агрегация"},
        { "isRight":true, "text":"обобщение"}
    ]
}'></div>

----

### Наследование

```typescript
class Student extends Person {
    constructor(name: string,
        public group: string
    ) { 
        super(name)
    }
    override toString = (): string => {
        return `${this.name}, гр. ${this.group}` } }
```

---

### Обозначение

![](inherit.svg)

---

### Плюсы и минусы наследования

```typescript
const ivan: Person = new Student("Иван", "22з")
console.log(`${ivan}`)
```
```typescript
Иван, гр. 22з 
```

---

<div class='quiz' data-quiz='{ 
    "question": "В каком виде связи классов переписываются свойства из одного класса в другой?",    
    "answers": [
        { "isRight":false, "text":"композиция"},
        { "isRight":true, "text":"наследование"},
        { "isRight":false, "text":"агрегация"},
        { "isRight":false, "text":"обобщение"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какое ключевое слово используется при наследовании класса?",    
    "answers": [
        { "isRight":false, "text":"implements"},
        { "isRight":true, "text":"extends"},
        { "isRight":false, "text":"abstract"},
        { "isRight":false, "text":"public"}
    ]
}'></div>

----

### Зависимость (реализация)

```typescript
interface Person {
    name: string
}
class Student implements Person {
    constructor( 
        public name: string,
        public group: string
    ) { }
    toString = (): string => {
        return `${this.name}, гр. ${this.group}` } }
```

---

### Обозначение

![](dependency.svg)

---

### Плюсы и минусы реализации

```typescript
const ivan: Person = new Student("Иван", "22з")
console.log(`${ivan}`)
```
```typescript
Иван, гр. 22з 
```

---

<div class='quiz' data-quiz='{ 
    "question": "Какое ключевое слово используется при реализации интерфейса?",    
    "answers": [
        { "isRight":true, "text":"implements"},
        { "isRight":false, "text":"extends"},
        { "isRight":false, "text":"abstract"},
        { "isRight":false, "text":"public"}
    ]
}'></div>