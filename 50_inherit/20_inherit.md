### Реализация классов

```typescript
class Person {
    constructor(public name: string) { }
    public toString = (): string => {
        return `${this.name}`
    }
}
class Student implements Person {
    name = "student"
}
```

---

### Наследование классов

```typescript
const ivan: Person = new Student("Иван", "22з")
class Person {
    constructor( public name: string ) { }
    public toString = (): string => {
        return `${this.name}` }}
class Student extends Person {
    constructor(
        name: string,
        public group: string
    ) { super(name) }
    override toString = (): string => {
        return `${this.name}, гр. ${this.group}`
    }}
```

---

### Наследование классами интерфейсов

```typescript
interface View {}
interface Action {}

class Person {
    constructor( public name: string ) { }
    public toString = (): string => {
        return `${this.name}` 
    } 
}
class Student extends View {
    constructor(name: string) {
        super(name)
    }
}
```
```
Не удается расширить интерфейс "View". 
Вы имели в виду "реализует"?ts(2689)
```

---

### Наследование интерфейсов

```typescript
interface View { }
interface Action { }
interface ViewAction extends View, Action {}
```

---

### Наследование и реализация 

```typescript
class Student extends Person implements View, Action {
    constructor( 
        name: string,
        public group: string
    ) { super(name) }
    override toString = (): string => {
        return `${this.name}, гр. ${this.group}` } 
    }
```

---

<div class='quiz' data-quiz='{ 
    "question": "После какого ключевого слово может идти перечисление элементов через запятую?",    
    "answers": [
        { "isRight":true, "text":"implements"},
        { "isRight":false, "text":"extends"},
        { "isRight":false, "text":"abstract"},
        { "isRight":false, "text":"public"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие ключевые слова записываются после имени класса?",    
    "answers": [
        { "isRight":true, "text":"implements"},
        { "isRight":true, "text":"extends"},
        { "isRight":false, "text":"abstract"},
        { "isRight":false, "text":"public"}
    ]
}'></div>

----

### Абстрактный класс

```typescript
abstract class Person {
    abstract name: string
    abstract print(): string 
}
class Student extends Person {
    constructor(
        public name: string,
        public group: string
    ) { super() }
    print(): string {
        return `${this.name}, гр. ${this.group}`
    } }
```

---

### Конструктор абстрактного класса

```typescript
abstract class Person {
    abstract name: string
    abstract print(): string 
}
class Student extends Person {
    constructor(
        public name: string,
        public group: string
    ) { super() }
    print(): string {
        return `${this.name}, гр. ${this.group}`
    } }
```

---

### Абстрактный класс и статические методы

```typescript
abstract class Person { ...
    static create(
        person: new (args: string[]) => Person,
        args: string[]
    ): Person { return new person(args) } }
class Student extends Person { ...
    constructor(args: string[]) {
        super()
        this.name=args[0]
        this.group=args[1] }
    print(): string {...}}
const ivan = Person.create(Student, ["Иван", "22з"])
console.log(ivan.print())
```

---

### Сигнатура конструктора

```typescript
abstract class Person { ...
    static create(
        person: new (args: string[]) => Person,
        args: string[]
    ): Person { return new person(args) } }
class Student extends Person { ...
    constructor(args: string[]) {
        super()
        this.name=args[0]
        this.group=args[1] }
    print(): string {...}}
const ivan = Person.create(Student, ["Иван", "22з"])
console.log(ivan.print())
```

---

<div class='quiz' data-quiz='{ 
    "question": "Перед чем из перечисленного может быть ключевое слово abstract?",    
    "answers": [
        { "isRight":true, "text":"класс"},
        { "isRight":true, "text":"поле"},
        { "isRight":true, "text":"метод"},
        { "isRight":false, "text":"конструктор"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какой код может вызывать конструктор абстрактного класса?",    
    "answers": [
        { "isRight":true, "text":"<code>super()</code>"},
        { "isRight":false, "text":"<code>super.constructor()</code>"},
        { "isRight":false, "text":"<code>abstract()</code>"},
        { "isRight":false, "text":"<code>constructor()</code>"}
    ]
}'></div>

----

### Интерфейсы 

- нет конструктора
- нет значений полей по умолчанию
- нет реализации метода
- допускают множественную реализацию

### Абстрактные классы

- есть конструктор
- могут быть заданы значения полей
- может быть задана реализация методов
- не допускает множественного наследования 

---

### Продвинутые интерфейсы

- допускают реализацию методов
- значение полей по умолчанию могут заданы с помощью геттеров

---

### Типаж (trait)

- не содержит полей
- допускает реализацию методов
- допускает множественную реализацию


---

### Примеси (mixin)

Класс, не предназначенный для создания объектов, реализует определенный аспект.
Ограничения примесей и реализация идеи различаются в различных языках.

---

<div class='quiz' data-quiz='{ 
    "question": "Что из перечисленного справедливо для интерфейсов?",    
    "answers": [
        { "isRight":false, "text":"Можно создавать объекты соответствующего типа"},
        { "isRight":true, "text":"Можно создавать ссылки на объекты соответствующего типа"},
        { "isRight":true, "text":"Для создание объектов требуется реализация свойств"},
        { "isRight":false, "text":"Есть конструктор"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Что из перечисленного справедливо для абстрактных классов?",    
    "answers": [
        { "isRight":false, "text":"Можно создавать объекты соответствующего типа"},
        { "isRight":true, "text":"Можно создавать ссылки на объекты соответствующего типа"},
        { "isRight":true, "text":"Для создание объектов требуется реализация свойств"},
        { "isRight":true, "text":"Есть конструктор"}
    ]
}'></div>