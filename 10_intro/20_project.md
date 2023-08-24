### Платформа Node.js

**Node.js** - кросс-платформенная среда выполнения JavaScript с открытым исходным кодом.

**Пакеты** Node.js - программные модули для платформы, библиотеки или утилиты.

**Менеджер пакетов** (**npm**, yarn, ..) - загружают нужную версию пакетов и его зависимостей.

**Стандарт (система) сборки** (**CommonJS**, **ES modules**) - определяют порядок импорта и соединяют код из различных файлов.

---

### npm

```
npm install --global typescript

npm list -g --depth=0

npm install
```

---

### JSON

```JSON
{
   "firstName": "Иван",
   "lastName": "Иванов",
   "address": {
       "streetAddress": "Московское ш., 101, кв.101",
       "city": "Ленинград",
       "postalCode": 101101
   },
   "phoneNumbers": [
       "812 123-1234",
       "916 123-4567"
   ]
}
```

---

### package.json

```JSON
{
  "scripts": {
    "start": "webpack serve --open",
    "dev": "webpack --mode development",
    "build": "webpack"
  },
  "devServer": {
    "static": "./dist"
  },
  "devDependencies": { ... }
}
```

---

### package.json

```JSON
{ ...
  "devDependencies": {
    "@types/jest": "^29.5.3",
    "html-webpack-plugin": "^5.5.3",
    "ts-jest": "^29.1.1",
    "ts-loader": "^9.4.3",
    "webpack": "^5.88.0",
    "webpack-cli": "^5.1.4",
    "webpack-dev-server": "^4.15.1"
  }
}
```

---

<div class='quiz' data-quiz='{ 
    "question": "Что указывает ключ <code>-g</code> в команде <code>node install</code>?",    
    "answers": [
        { "isRight":false, "text":"Будут установлены пакеты указанные в файле <code>package.json</code>"},
        { "isRight":true, "text":"Пакеты будут установлены глобально"},
        { "isRight":false, "text":"Пакеты будут установлены в текущей проект"}
    ]
}'></div>

---

<div class='quiz' data-quiz='{ 
    "question": "Какие скобки в формате JSON используются для массивов?",    
    "answers": [
        { "isRight":false, "text":"{}"},
        { "isRight":true, "text":"[]"},
        { "isRight":false, "text":"()"},
        { "isRight":false, "text":"<>"}
    ]
}'></div>


----

### Webpack

- сборщик модулей Web-приложений


---

### webpack.config.js

```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
    mode: "development",
    entry: './src/index.ts',
    devtool: 'inline-source-map',
    module: {
        rules: [{
                test: /\.tsx?$/,
                use: 'ts-loader',
                exclude: /node_modules/,
            },],
    }, ... };
```

---

### webpack.config.js

```javascript
...
module.exports = {
    ...
    resolve: {
        extensions: ['.tsx', '.ts', '.js'],
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: 'src/index.html'
        }), ],
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, 'dist'),
    },};
```

---

<div class='quiz' data-quiz='{ 
    "question": "Файлы с какими расширениями могут появлятся при работе webpack?",    
    "answers": [
        { "isRight":true, "text":"<code>css</code>"},
        { "isRight":true, "text":"<code>js</code>"},
        { "isRight":true, "text":"<code>html</code>"},
        { "isRight":false, "text":"<code>ts</code>"}
    ]
}'></div>

----

### Компилятор typescript

```
tsc hello.ts

webpack
```

---

### tsconfig.json

```JSON
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "lib": [ "es6", "dom", "es2017" ],
    "strict": true,
    "declaration": true,
    "outDir": "dist",
    "sourceMap": true,
    "noImplicitOverride": true
  },
  ... 
}
```

---

### tsconfig.json

```JSON
{
  ...
  "include": [
    "src/*"
  ],
  "exclude": [
    "node_modules",
    "src/*.spec.ts"
  ]
}
```

---

<div class='quiz' data-quiz='{ 
    "question": "Для указания чего используется ключ <code>target</code> в <code>compilerOptions</code>?",    
    "answers": [
        { "isRight":true, "text":"версии javascript"},
        { "isRight":false, "text":"расположения скомпилированного файла"},
        { "isRight":false, "text":"рабочая или отладочная версия"},
        { "isRight":false, "text":"тип используемого транлятора языков"}
    ]
}'></div>


----

### Компиляция и запуск на nodejs

```src/index.ts```
```typescript
const message = 'Привет мир!'
console.log(message)
```

---

### Компиляция

```
tsc
```

```dist/index.js```

```javascript
"use strict";
var message = 'Привет мир!';
console.log(message);
//# sourceMappingURL=index.js.map
```

---

### Запуск

```
node .\dist\index.js
Привет мир!
```

---

<div class='quiz' data-quiz='{ 
    "question": "Где можно указать имена файлов для компиляции командой <code>tsc</code>?",    
    "answers": [
        { "isRight":true, "text":"после имени команды"},
        { "isRight":true, "text":"в файле <code>tsconfig.json</code>"},
        { "isRight":false, "text":"в файле <code>package.json</code>"},
        { "isRight":false, "text":"после команды <code>node</code>"}
    ]
}'></div>


----

### Компиляция и запуск в браузере

```src/index.html```
```html
<!doctype html>

<head>
    <meta charset="UTF-8">
    <title>App</title>
</head>

<body>
    <div id="root">
    </div>
</body>

</html>
```

---

### Сборка

```
npm run start

> start
> webpack serve --open

<i> [webpack-dev-server] Project is running at:
<i> [webpack-dev-server] Loopback: http://localhost:8080/
<i> [webpack-dev-server] On Your Network (IPv4): http://192.168.0.109:8080/
<i> [webpack-dev-server] Content not from webpack is served from 'C:\work\project\public' directory
<i> [webpack-dev-middleware] wait until bundle finished: /
...
webpack 5.88.2 compiled successfully in 1709 ms
```

---

### Запуск

![](run_in_browser.jpg)

---

<div class='quiz' data-quiz='{ 
    "question": "Какими командами <code>npm</code> можно начать отладку в браузере?",    
    "answers": [
        { "isRight":true, "text":"<code>run start</code>"},
        { "isRight":true, "text":"<code>webpack serve --open</code>"},
        { "isRight":false, "text":"<code>run dev</code>"},
        { "isRight":false, "text":"<code>webpack browser</code>"}
    ]
}'></div>