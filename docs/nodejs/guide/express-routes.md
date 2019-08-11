# Маршрутизация

При обработке запросов фреймворк Express опирается на систему маршрутизации. В приложении определяются маршруты, а также обработчики этих маршрутов. Если запрос соответствует определенному маршруту, то вызывается для обработки запроса соответствующий обработчик.

Для обработки данных по определенному маршруту можно использовать ряд функций, в частности:

- `use`
- `get`
- `post`
- `put`
- `delete`

В качестве первого параметра эти функции могут принимать шаблон адреса, запрос по которому будет обрабатываться. Второй параметр функций представляет функцию, которая будет обрабатывать запрос по совпавшему с шаблоном адресу. Например:

```js
const express = require('express')
const app = express()

// обработка запроса по адресу /about
app.get('/about', function(request, response) {
  response.send('<h1>О сайте</h1>')
})

// обработка запроса по адресу /contact
app.use('/contact', function(request, response) {
  response.send('<h1>Контакты</h1>')
})

// обработка запроса к корню веб-сайта
app.get('/', function(request, response) {
  response.send('<h1>Главная страница</h1>')
})
app.listen(3000)
```

Когда приходит запрос Express сопоставляет запрошенный адрес с каждым из маршрутов. Затем выбирается первый совпавший маршрут. При совпадении маршрута вызывается его функция обработчика.

Но при определении функции для обработки того или иного машрута следует учитывать, что более общие маршруты должны идти после более частных. Так, в примере выше сначала идут функции для обработки маршрутов `/contact` и `/about` и лишь затем функции для обработки корневного маршрута `/`, поскольку маршруты `/contact` и `/about` содержат маршрут `/`. Поэтому node.js маршрут `/` может интерпретировть и как `/contact`, и как `/about`.

## Символы подстановок

Используемые шаблоны адресов могут содержать регулярные выражения или специальные символы подстановок. В частности, мы можем использовать такие символы, как `?`, `+`, `*` и `()`.

К примеру, символ `?` указывает, что предыдущий символ может встречаться 1 раз или отсутствовать. И мы можем определить следующую функцию:

```js
app.get('/bo?k', function(request, response) {
  response.send(request.url)
})
```

Такой маршрут будет соответствовать строке запроса `/bk` или `/bok`.

Символ `+` указывает, что предыдущий символ может встречаться 1 и более раз:

```js
app.get('/bo+k', function(request, response) {
  response.send(request.url)
})
```

Такой маршрут будет соответствовать запросам `/bok`, `/book`, `/boook` и так далее.

Символ звездочка `*` указывает, что на месте данного символа может находиться любое количество символов:

```js
app.get('/bo*k', function(request, response) {
  response.send(request.url)
})
```

Такой маршрут будет соответствовать запросам `/bork`, `/bonk`, `/bor.dak`, `/bor/ok` и так далее.

Скобки `()` позволяют оформить группу символов, которые могут встречаться в запросе:

```js
app.get('/book(.html)?', function(request, response) {
  response.send(request.url)
})
```

Выражение `(.html)?` указывает, что подстрока `.html` может встречаться или отсутствовать в строке запроса. И такой маршрут будет соответствовать запросам `/book` и `/book.html`.

Также вместо определения маршрутов мы можем указывать регулярные выражения. Например, необходимо перехватить запрос ко всем файлам html или всем путям, которые в конце имеют `.html`:

```js
app.get(/.*(\.)html$/, function(request, response) {
  response.send(request.url)
})
```