# JavaScript и Node.js

## JavaScript и Вы

До того как мы поговорим о технических вещах, позвольте занять некоторое время и поговорить о вас и ваших отношениях с JavaScript. Эта глава позволит вам понять, имеет ли смысл читать дальше.

Скорее всего, как и в моем случае, вы начали свой путь в веб-разработке с написания простых статических HTML-документов. Вместе с этим, вы познакомились с веселой штукой, называемой [JavaScript](/javascript/), но использовали его исключительно в простых случаях, добавляя интерактивности на ваши веб-странички.

Что вы хотели узнать — так это действительно полезные вещи; вы хотели знать, как создать сложный сайт. Для этого вы изучали [PHP](/php/), Ruby, Java и начинали писать backend-код.

Тем не менее, вы постоянно следили за JavaScript, вы видели, что с появлениям [JQuery](/jquery/), Prototype и других фреймворков этот язык стал больше, чем просто `window.open()`.

Однако, это всё ещё относилось к frontend-разработке. Конечно, jQuery — очень мощный инструмент, но всякий раз, когда вы приправляли ваш сайт разными jQuery-«фишками», в лучшем случае, вы были JavaScript-пользователем нежели JavaScript-разработчиком.

А потом пришел Node.js. JavaScript на сервере: насколько это хорошо?

И вы решили, что пора проверить старый новый JavaScript. Подождите. Написать Node.js приложение — одно дело, а понять, почему оно должно быть написано таким образом, для этого нужно понимать JavaScript. И на этот раз — по-настоящему.

В этом — как раз и проблема. JavaScript живёт двумя, может даже тремя разными жизнями: весёлый маленький DHMTL-помощник из середины 90-х годов, более серьезный frontend-инструмент в лице jQuery и наконец серверный (server-side, backend) JavaScript. По этой причине не так просто найти информацию, которая поможет вам познать правильный JavaScript, пригодный для написания Node.js приложения в манере, дающий ощущение, что вы не просто использовали JavaScript, а действительно разрабатывали на JavaScript.

Это — наиболее правильный подход. Вы — уже опытный разработчик, вы не хотите изучать новые технологии поверхностно, просто валяя дурака. Вы хотите быть уверенным, что вы подходите к проблеме под правильным углом.

Конечно, существует отличная документация по Node.js, но её зачастую недостаточно. Нужно руководство.

Моя цель заключается в обеспечении вас руководством.

## Предупреждение

Существуют действительно отличные специалисты в области JavaScript. Я не из их числа.

Я — действительно, тот парень, о котором написано в предыдущем параграфе. Я знаю кое-что о разработке backend веб-приложений, но я всё ещё новичок в «реальном» JavaScript и всё ещё новичок в Node.js. Я узнал некоторые продвинутые аспекты JavaScript совсем недавно. Я неопытен.

Вот почему эта книга не из разряда «от новичка к эксперту», а скорее «от новичка к продвинутому новичку».

Если всё удастся, то этот документ станет тем руководством, которое я хотел бы иметь, когда начинал в Node.js.

## Server-side JavaScript

Первая инкарнация JavaScript жила в теле браузера. Но это всего лишь контекст. Он определяет, что вы можете делать с языком, но не говорит о том, что язык сам по себе может сделать. JavaScript это «полноценный» язык: вы можете использовать его в различных контекстах и достичь всего того, что можете достичь с другими «полноценными» языками.

Node.js — действительно, просто другой контекст: он позволяет вам запускать JavaScript-код вне браузера.

Чтобы ваш JavaScript код выполнился на вычислительной машине вне браузера (на backend), он должен быть интерпретирован и, конечно же, выполнен. Именно это и делает Node.js. Для этого он использует движок V8 VM от Google — ту же самую среду исполнения для JavaScript, которую использует браузер Google Chrome.

Кроме того, Node.js поставляется со множеством полезных модулей, так что вам не придется писать всё с нуля, как, например, вывод строки в консоль.

Таким образом, Node.js состоит из 2 вещей: среды исполнения и полезных библиотек.

Для того чтобы их использовать, вам необходимо установить Node.js. Вместо повторения всего процесса установки здесь, я просто приглашу вас посетить официальную инструкцию по инсталляции. Пожалуйста, вернитесь обратно после успешной установки.

## «Hello world»

Хорошо, давайте пойдём сразу с места в карьер и напишем наше первое Node.js-приложение: «Hello world».

Откройте ваш любимый редактор и создайте файл под названием `helloworld.js`. Мы хотим вывести строку «Hello world» в консоль, для этого пишем следующий код:

```js
console.log('Hello World')
```

Сохраняем файл и выполняем его посредством Node.js:

```bash
node helloworld.js
```

Это должно вывести Hello World на наш терминал.

Ладно, всё это скучно, правда? Давайте напишем что-нибудь полезное.
