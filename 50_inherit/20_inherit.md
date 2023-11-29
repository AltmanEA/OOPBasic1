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
