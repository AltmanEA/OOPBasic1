### Пример класса

```typescript
class Student {
    first_name: string
    last_name: string
}
const ivan = new Student()
ivan.first_name = "Иван", 
ivan.last_name = "Иванов"
console.log(ivan.first_name, ivan.last_name)
```
```typescript
Иван Иванов
```

---

### Конструктор класса

```typescript
class Student {
    first_name: string
    last_name: string
    constructor(first_name: string, last_name: string) {
        this.first_name = first_name
        this.last_name = last_name
    }
}
const ivan = new Student("Иван", "Иванов")
console.log(ivan.first_name, ivan.last_name)
```
```typescript
Иван Иванов
```

---

### Поля класса

```typescript
class Student {
    readonly first_name: string
    readonly last_name: string            
    constructor(first_name: string, last_name: string) {
        this.first_name = first_name
        this.last_name = last_name
        this.full_name = `${first_name} ${last_name}`
    }
    lesson = 0
    full_name: string
}
const ivan = new Student("Иван", "Иванов")
console.log(ivan.full_name, ivan.lesson)
```
```typescript
Иван Иванов 0
```

---

### Методы класса

```typescript
class Student {
    first_name: string
    last_name: string            
    constructor(first_name: string, last_name: string) {
        this.first_name = first_name
        this.last_name = last_name
    }
    full_name(): string{
        return `${this.first_name} ${this.last_name}`
    }
}
const ivan = new Student("Иван", "Иванов")
console.log(ivan.full_name())
```
```typescript
Иван Иванов
```

---

<div class='quiz' data-quiz='{ 
    "question": "Для чего из перечисленного не нужно указывать тип значения?",    
    "answers": [
        { "isRight":true, "text":"конструктор"},
        { "isRight":false, "text":"функция"},
        { "isRight":false, "text":"метод"},
        { "isRight":false, "text":"поле"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Где могут инициализироваться поля класса?",    
    "answers": [
        { "isRight":true, "text":"при объявлении"},
        { "isRight":true, "text":"в конструкторе"},
        { "isRight":false, "text":"в методе, объявленном раньше поля"},
        { "isRight":false, "text":"в методе, объявленном позже поля"}
    ]
}'></div>

----

### Перегрузка конструктора

```typescript
    constructor(full_name: string)
    constructor(names: [string, string])
    constructor(name: string | [string, string]) {
        if (typeof name === "string") {
            const tmp = name.split(" ")
            this.first_name = tmp[0]
            this.last_name = tmp[1]
        } else {
            this.first_name = name[0]
            this.last_name = name[1]
        }}
        
console.log(new Student(["Иван", "Иванов"]).full_name())
console.log(new Student("Петр Петров").full_name())
```
```typescript
Иван Иванов
Петр Петров
```

---

### Копирующий конструктор

```typescript
    copy(): Student{
        return new Student(this.full_name())
    }
const ivan = new Student(["Иван", "Иванов"])
const ivan2 = ivan.copy()
console.log(ivan)
console.log(ivan2)
console.log(ivan===ivan2)    
```
```typescript
Student { first_name: 'Иван', last_name: 'Иванов' }
Student { first_name: 'Иван', last_name: 'Иванов' }
false
```

---

### Фабричный (виртуальный) конструктор

```typescript
    create(full_name: string): Student | null {
        const tmp = full_name.split(" ")
        if(tmp.length!==2)
            return null
        return  new Student(full_name)
    }
const ivan = new Student(["Иван", "Иванов"])
const petr = ivan.create("Петр Петров")
const anon = ivan.create("Аноним")
console.log(ivan)
console.log(petr)
console.log(anon)        
```
```typescript
Student { first_name: 'Иван', last_name: 'Иванов' }
Student { first_name: 'Петр', last_name: 'Петров' }
null
```

---

### Использование методов в конструкторе

```typescript
    constructor(full_name: string)
    constructor(names: [string, string])
    constructor(name: string | [string, string]) {
        if (typeof name === "string") {
            const tmp = name.split(" ")
            this.first_name = tmp[0]
            this.last_name = tmp[1]
        } else {
            const fn = this.full_name().split(" ")
            this.first_name = fn[0]
            this.last_name = fn[1]
        }}
console.log(new Student(["Иван", "Иванов"]))
console.log(new Student("Петр Петров"))
```
```typescript
Student { first_name: 'undefined', last_name: 'undefined' }
Student { first_name: 'Петр', last_name: 'Петров' }
```

---

<div class='quiz' data-quiz='{ 
    "question": "Что из перечисленного можно делать в TS?",    
    "answers": [
        { "isRight":true, "text":"перегружать конструктор"},
        { "isRight":false, "text":"создавать вторичный конструктор"},
        { "isRight":true, "text":"вызывать в конструкторе методы класса "},
        { "isRight":false, "text":"возвращать null  в конструкторе"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какой тип конструкторов может вернуть <code>null</code> при некорректных аргументах?",    
    "answers": [
        { "isRight":false, "text":"обычный"},
        { "isRight":true, "text":"фабричный"},
        { "isRight":false, "text":"копирующий"},
        { "isRight":false, "text":"вторичный"}
    ]
}'></div>


----

### Статический конструктор

```typescript
    static create(full_name: string): Student | null {
        const tmp = full_name.split(" ")
        if(tmp.length!==2)
            return null
        return  new Student(full_name)
    } 
const ivan = new Student(["Иван", "Иванов"])
const petr = Student.create("Петр Петров")
const anon = Student.create("Аноним")
console.log(ivan)  
console.log(petr)
console.log(anon)        
```
```typescript
Student { first_name: 'Иван', last_name: 'Иванов' }
Student { first_name: 'Петр', last_name: 'Петров' }
null
```

---

### Статический метод

```typescript
    static who_i(): typeof Student{
        return this
    }
    
console.log(Student.who_i())    
```
```typescript
// es5
[Function: Student] {
  create: [Function (anonymous)],
  who_i: [Function (anonymous)]
}
```
```typescript
// es6
[class Student]
```

---

### Класс во время исполнения

```typescript
const x = Student
console.log(x)
```
```typescript
// es5
[Function: Student] {
  create: [Function (anonymous)],
  who_i: [Function (anonymous)]
}
```
```typescript
// es6
[class Student]
```

---

<div class='quiz' data-quiz='{ 
    "question": "Где находятся статические методы класса?",    
    "answers": [
        { "isRight":false, "text":"в самом классе"},
        { "isRight":true, "text":"в отдельном объекте, связанным с классом"},
        { "isRight":false, "text":"в глобальном контексте"},
        { "isRight":false, "text":"в прототипе"}
    ]
}'></div>

----

### Реализация класса в JS (es5)

```typescript
var Student = /** @class */ (function () {
    function Student(name) {
        if (typeof name === "string") {
            var tmp = name.split(" ");
            this.first_name = tmp[0];
            this.last_name = tmp[1];
        }
        else {
            this.first_name = name[0];
            this.last_name = name[1];
        }
    }
```

---

### Реализация класса в JS (es5)

```typescript
    Student.prototype.copy = function () {
        return new Student(this.full_name());
    };
    Student.create = function (full_name) {
        var tmp = full_name.split(" ");
        if (tmp.length !== 2)
            return null;
        return new Student(full_name);
    };
```

---

### Реализация класса в JS (es5)

```typescript
    Student.prototype.full_name = function () {
        return "".concat(this.first_name, " ").concat(this.last_name);
    };
    Student.who_i = function () {
        return this;
    };
    return Student;
}());
```

---

<div class='quiz' data-quiz='{ 
    "question": "Где находятся методы класса после компиляции в ES5?",    
    "answers": [
        { "isRight":false, "text":"в самом классе"},
        { "isRight":false, "text":"в отдельном объекте, связанным с классом"},
        { "isRight":false, "text":"в глобальном контексте"},
        { "isRight":true, "text":"в прототипе"}
    ]
}'></div>