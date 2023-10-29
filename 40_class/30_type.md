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

----

### Обобщенные типы (Generic)

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
console.log(ivan, petr)
```
```typescript
Student { name: 'Иван', group: '22з' } Tutor { name: 'Петр', dep: 'Мат' }
```