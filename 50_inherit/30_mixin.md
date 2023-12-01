### Базовый класс

```typescript
class Sprite {
    x = 0
    y = 0
    constructor(
        public name: string = ""
    ) { }
}
```

---

### Примесь

```typescript
type Constructor = new (...args: any[]) => any;
function Scale<TBase extends Constructor>(Base: TBase) {
  return class Scaling extends Base {
    _scale = 1
     setScale(scale: number): void {
      this._scale = scale
    }
     get scale(): number {
      return this._scale
    }
  }
}
```

---

### Базовый класс с примесью

```typescript
// const ScaledSprite: {
//    new (...args: any[]): Scale<typeof Sprite>.Scaling;
//    prototype: Scale<any>.Scaling;
// } & typeof Sprite
const ScaledSprite = Scale(Sprite)
// const object: Scale<typeof Sprite>.Scaling & Sprite
const object = new ScaledSprite("")
object.setScale(0.8)
console.log(object.scale)
```

---

### Ограничение на базовый класс

```typescript
type GConstructor<T = {}> = new (...args: any[]) => T;
type Positionable = GConstructor<{
    setPos: (x: number, y: number) => void
}>
type Spritable = GConstructor<Sprite>
type Loggable = GConstructor<{ print: () => void }>
function Jumpable<TBase extends Positionable>(Base: TBase) {
    return class Jumpable extends Base {
      jump() {
        this.setPos(0, 20)
      }
    }
  }
```

----

### Примеси JS

```typescript
class Jumpable {
    jump() { }
}
class Duckable {
    duck() { }
}
class Sprite {
    x = 0;
    y = 0;
}
interface Sprite extends Jumpable, Duckable { }
```

---

### Функция для добавления примесей

```typescript
function applyMixins(derivedCtor: any, constructors: any[]) {
    constructors.forEach((baseCtor) => {
Object.getOwnPropertyNames(baseCtor.prototype)
    .forEach((name) => {
        Object.defineProperty(
            derivedCtor.prototype,
            name,
            Object.getOwnPropertyDescriptor(
                baseCtor.prototype, name) ||
            Object.create(null) ) })
    })
}
```

---

### Применение примесей JS

```typescript
applyMixins(Sprite, [Jumpable, Duckable])
 
let player = new Sprite();
player.jump()
console.log(player.x, player.y)
```

----

### Декоратор метода

```typescript
function loggedMethod(
  originalMethod: any, 
  context: ClassMethodDecoratorContext) {
    const methodName = String(context.name);
    function replacementMethod(this: any, ...args: any[]) {
        console.log(`LOG: Entering method '${methodName}'.`)
        const result = originalMethod.call(this, ...args);
        console.log(`LOG: Exiting method '${methodName}'.`)
        return result }
    return replacementMethod
}
```

---

### Декоратор метода

```typescript
class Person {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    @loggedMethod
    greet() {
        console.log(`Hello, my name is ${this.name}.`);
    }
}
const p = new Person("Ron");
p.greet();
```
```
LOG: Entering method.
Hello, my name is Ron.
LOG: Exiting method.
```

---

### Декоратор 

```typescript
type SyntheticDecorator<T, C, R> = 
  (target: T, context: C) => R | void
```



