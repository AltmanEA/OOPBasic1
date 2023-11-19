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

----

### Обобщение

![](template.svg)

---

### Плюсы и минусы обобщения

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