# Собеседование по TypeScript: 20 вопросов и ответов

Язык TypeScript основан на том же синтаксисе и семантике, которые хорошо знакомы миллионам JavaScript-разработчиков. TypeScript даёт возможность работать с самыми свежими и ещё только появляющимися возможностями JS, включая те, которые имеются в ECMAScript 2015, и те, которые пока существуют лишь в виде предложений. Среди таких возможностей, например, асинхронные функции и декораторы. Всё это направлено на то, чтобы помочь разработчику в создании надёжных и современных приложений.

TypeScript-программа компилируется в обычный JavaScript-код, который может выполняться в любом браузере или в среде Node.js. Этот код будет понятен любому JS-движку, который поддерживает стандарт ECMAScript 3 или более новый.

Материал, перевод которого мы сегодня публикуем, содержит разбор двадцати вопросов, которые вполне могут задать тому, кто собирается пройти собеседование, претендуя на позицию TypeScript-программиста.

??? faq "1. Что такое TypeScript и зачем использовать его вместо JavaScript"

    _В скобках, после номера вопроса, указана его сложность, оцениваемая по пятибалльной шкале._

    TypeScript (TS) – это надмножество JavaScript (JS), среди основных особенностей которого можно отметить возможность явного статического назначения типов, поддержку классов и интерфейсов. Одним из серьёзных преимуществ TS перед JS является возможность создания, в различных IDE, такой среды разработки, которая позволяет, прямо в процессе ввода кода, выявлять распространённые ошибки. Применение TypeScript в больших проектах может вести к повышению надёжности программ, которые, при этом, можно разворачивать в тех же средах, где работают обычные JS-приложения.

    Вот некоторые подробности о TypeScript:

    TypeScript поддерживает современные редакции стандартов ECMAScript, код, написанный с использованием которых, компилируется с учётом возможности его выполнения на платформах, поддерживающих более старые версии стандартов. Это означает, что TS-программист может использовать возможности ES2015 и более новых стандартов, наподобие модулей, стрелочных функций, классов, оператора spread, деструктурирования, и выполнять то, что у него получается, в существующих средах, которые пока этих стандартов не поддерживают.

    TypeScript – это надстройка над JavaScript. Код, написанный на чистом JavaScript, является действительным TypeScript-кодом.

    TypeScript расширяет JavaScript возможностью статического назначения типов. Система типов TS отличается довольно обширными возможностями. А именно, она включает в себя интерфейсы, перечисления, гибридные типы, обобщённые типы (generics), типы-объединения и типы-пересечения, модификаторы доступа и многое другое. Применение TypeScript, кроме того, немного упрощает работу за счёт использования вывода типов.

    Применение TypeScript, в сравнении с JavaScript, значительно улучшает процесс разработки. Дело в том, что IDE, в реальном времени, получает сведения о типах от TS-компилятора.

    При использовании режима строгой проверки на `null` (для этого применяется флаг компилятора `--strictNullChecks`), компилятор TypeScript не разрешает присвоение `null` и `undefined` переменным тех типов, в которых, в таком режиме, использование этих значений не допускается.

    Для использования TypeScript нужно организовать процесс сборки проекта, включающий в себя этап компиляции TS-кода в JavaScript. Компилятор может встроить карту кода (source map) в сгенерированные им JS-файлы, или создавать отдельные .map-файлы. Это позволяет устанавливать точки останова и исследовать значения переменных во время выполнения программ, работая непосредственно с TypeScript-кодом.

    TypeScript — это опенсорсный проект Microsoft, выпущенный под лицензией Apache 2. Инициатором разработки TypeScript является Андерс Хейлсберг. Он причастен к созданию Turbo Pascal, Delphi и C#.

??? faq "2. Расскажите об обобщённых типах в TypeScript"

    Обобщённые типы (generics) позволяют создавать компоненты или функции, которые могут работать с различными типами, а не с каким-то одним. Рассмотрим пример:

    ```ts
    /** Объявление класса с параметром обобщённого типа */
    class Queue<t> {
    private data = []
    push = (item: T) => this.data.push(item)
    pop = (): T => this.data.shift()
    }

    const queue = new Queue<number>()
    queue.push(0)
    queue.push('1') // Ошибка : в такую очередь нельзя добавить строку, тут разрешено использовать лишь числа
    ```

??? faq "3. Поддерживает ли TypeScript все принципы объектно-ориентированного программирования"

    Да, поддерживает. Существуют четыре основных принципа объектно-ориентированного программирования:

    - Инкапсуляция
    - Наследование
    - Абстракция
    - Полиморфизм

    Пользуясь простыми и понятными средствами TypeScript, можно реализовать все эти принципы.

??? faq "4. Как в TypeScript проверять значения на равенство null и undefined"

    Для выполнения подобных проверок достаточно воспользоваться следующей конструкцией:

    ```ts
    if (value) {
    }
    ```

    Выражение в скобках будет приведено к `true` в том случае, если оно не является чем-то из следующего списка:

    - null
    - undefined
    - NaN
    - Пустая строка
    - 0
    - false

    TypeScript поддерживает те же правила преобразования типов, что и JavaScript.

??? faq "5. Как в TypeScript реализовать свойства класса, являющиеся константами"

    В TypeScript, при объявлении свойств классов, нельзя использовать ключевое слово `const`. При попытке использования этого ключевого слова выводится следующее сообщение об ошибке: A class member cannot have the ‘const’ keyword. В TypeScript 2.0 имеется модификатор `readonly`, позволяющий создавать свойства класса, предназначенные только для чтения:

    ```ts
    class MyClass {
    readonly myReadonlyProperty = 1

    myMethod() {
    	console.log(this.myReadonlyProperty)
    }
    }

    new MyClass().myReadonlyProperty = 5 // ошибка, так как свойство предназначено только для чтения
    ```

??? faq "6. Что представляют собой .map-файлы в TypeScript"

    Файлы с расширением `.map` хранят карты кода (source map), которые содержат данные о соответствии кода, написанного на TypeScript, JavaScript-коду, созданному на его основе. С этим файлами могут работать многие отладчики (например — Visual Studio и инструменты разработчика Chrome). Это позволяет, в ходе отладки, работать с исходным кодом программ на TypeScript, а не с их JS-эквивалентами.

??? faq "7. Что такое геттеры и сеттеры в TypeScript"

    TypeScript поддерживает геттеры и сеттеры, которые позволяют управлять доступом к членам объектов. Они дают разработчику средства контроля над чтением и записью свойств объектов.

    ```ts
    class foo {
    private _bar: boolean = false

    get bar(): boolean {
    	return this._bar
    }
    set bar(theBar: boolean) {
    	this._bar = theBar
    }
    }

    var myBar = myFoo.bar // здесь вызывается геттер
    myFoo.bar = true // здесь вызывается сеттер
    ```

??? faq "8. Можно ли использовать TypeScript в серверной разработке, и если да — то как"

    Программы, написанные на TypeScript, подходят не только для фронтенд-разработки, но и для создания серверных приложений. Например, на TS можно писать программы для платформы Node.js. Это даёт программисту дополнительные средства по контролю типов и позволяет использовать другие возможности языка. Для создания серверных приложений на TS нужно лишь наладить правильный процесс обработки кода, на вход которого поступают TypeScript-файлы, а на выходе получаются JavaScript-файлы, подходящие для выполнения их в Node.js. Для того чтобы организовать такую среду, сначала надо установить компилятор TypeScript:

    ```bash
    npm i -g typescript
    ```

    Параметры компилятора задают с помощью файла `tsconfig.json`, который определяет, кроме прочего, цель компиляции и место, в которое нужно поместиться готовые JS-файлы. В целом, этот файл очень похож на конфигурационные файлы babel или webpack:

    ```json
    {
    "compilerOptions": {
    	"target": "es5",
    	"module": "commonjs",
    	"declaration": true,
    	"outDir": "build"
    }
    }
    ```

    Теперь, при условии, что компилятору есть что обрабатывать, нужно его запустить:

    ```bash
    tsc
    ```

    И, наконец, учитывая то, что JS-файлы, пригодные для выполнения в среде Node.js, находятся в папке `build`, надо выполнить такую команду, находясь в корневой директории проекта:

    ```bash
    node build/index.js
    ```

??? faq "9. Расскажите об основных компонентах TypeScript"

    TypeScript включает в себя три основных компонента:

    - **Язык.** Это, с точки зрения разработчиков, самая важная часть TypeScript. «Язык» — это синтаксис, ключевые слова, всё то, что позволяет писать программы на TypeScript.
    - **Компилятор.** TypeScript обладает компилятором с открытым исходным кодом, он является кросс-платформенным, с открытой спецификацией, и написан на TypeScript. Компилятор выполняет преобразование TypeScript-кода в JavaScript-код. Кроме того, если с программой что-то не так, он выдаёт сообщения об ошибках. Он позволяет объединять несколько TypeScript-файлов в один выходной JS-файл и умеет создавать карты кода.
    - **Вспомогательные инструменты.** Вспомогательные инструменты TypeScript предназначены для облегчения процесса разработки с его использованием в различных IDE. Среди них — Visual Studio, VS Code, Sublime, различные средства для быстрого запуска TS-кода, и другие.

??? faq "10. Есть ли в предоставленном вам TypeScript-коде ошибки? Объясните свой ответ"

    Вот фрагмент кода:

    ```ts
    class Point {
    x: number
    y: number
    }

    interface Point3d extends Point {
    z: number
    }

    let point3d: Point3d = { x: 1, y: 2, z: 3 }
    ```

    Ошибок в этом коде нет. Объявление класса создаёт две сущности: это тип данных, используемый для создания экземпляров класса, и функция-конструктор. Так как классы создают типы данных, использовать их можно там же, где можно использовать интерфейсы.

??? faq "11. Расскажите об использовании декораторов свойств в TypeScript"

    Декораторы можно использовать для изменения поведения классов, при этом ещё больше пользы от них можно получить при их использовании с каким-либо фреймворком. Например, если в вашем фреймворке есть методы, доступ к которым ограничен (скажем, они предназначены только для администратора), несложно будет написать декоратор метода @admin, который будет запрещать доступ к соответствующим методам пользователям, не являющимся администраторами. Можно создать декоратор `@owner`, который позволяет модифицировать объект только его владельцу. Вот как может выглядеть использование декораторов:

    ```ts
    class CRUD {
    	get() {}
    	post() {}

    	@admin
    	delete() {}

    	@owner
    	put() {}
    }
    ```

??? faq "12. Можно ли в TypeScript использовать строго типизированные функции в качестве параметров"

    Рассмотрим следующий пример:

    ```ts
    class Foo {
    save(callback: Function): void {
    	//Выполняем сохранение
    	var result: number = 42 //Получаем в ходе операции сохранения некое число
    	//Можно ли во время выполнения программы как-то обеспечить то, чтобы коллбэк принимал лишь один параметр типа number?
    	callback(result)
    }
    }

    var foo = new Foo()
    var callback = (result: string): void => {
    alert(result)
    }
    foo.save(callback)
    ```

    Можно ли в методе `save` организовать работу с типизированным коллбэком? Перепишите код для того, чтобы это продемонстрировать.

    В TypeScript можно объявить тип коллбэка, после чего переписать код:

    ```ts
    type NumberCallback = (n: number) => any

    class Foo {
    // Эквивалент
    save(callback: NumberCallback): void {
    	console.log(1)
    	callback(42)
    }
    }

    var numCallback: NumberCallback = (result: number): void => {
    console.log('numCallback: ', result.toString())
    }

    var foo = new Foo()
    foo.save(numCallback)
    ```

??? faq "13. Как сделать так, чтобы классы, объявленные в модуле, были бы доступны и за пределами этого модуля?"

    Классы, объявленные в модуле, доступны в пределах этого модуля. За его пределами доступ к ним получить нельзя.

    ```ts
    module Vehicle {
    class Car {
    	constructor(public make: string, public model: string) {}
    }
    var audiCar = new Car('Audi', 'Q7')
    }
    // Это работать не будет
    var fordCar = Vehicle.Car('Ford', 'Figo')
    ```

    В коде, приведённом выше, при попытке инициализации переменной `fordCar` произойдёт ошибка. Для того чтобы сделать класс, объявленный в модуле, доступным за пределами этого модуля, нужно воспользоваться ключевым словом `export`:

    ```ts
    module Vehicle {
    export class Car {
    	constructor(public make: string, public model: string) {}
    }
    var audiCar = new Car('Audi', 'Q7')
    }
    // Теперь этот фрагмент кода работает нормально
    var fordCar = Vehicle.Car('Ford', 'Figo')
    ```

??? faq "14 (3). Поддерживает ли TypeScript перегрузку функций"

    TypeScript поддерживает перегрузку функций, но реализация этого механизма отличается от той, которую можно видеть в других объектно-ориентированных языках. А именно, в TS создают лишь одну функцию и некоторое количество объявлений. Когда такой код компилируется в JavaScript, видимой оказывается лишь одна конкретная функция. Этот механизм работает из-за того, что JS-функции можно вызывать, передавая им разное количество параметров.

    ```ts
    class Foo {
    myMethod(a: string)
    myMethod(a: number)
    myMethod(a: number, b: string)
    myMethod(a: any, b?: string) {
    	alert(a.toString())
    }
    }
    ```

??? faq "15 (4). Что не так с предоставленным вам кодом"

    Вот код, о котором идёт речь:

    ```ts
    interface Fetcher {
    getObject(done: (data: any, elapsedTime?: number) => void): void
    }
    ```

    Рекомендуется использовать необязательные параметры в коллбэках только в том случае, если вы абсолютно точно понимаете последствия такого шага. Этот код имеет весьма специфический смысл: коллбэк `done` может быть вызван или с 1 или 2 аргументами. Автор кода, вероятно, намеревался сообщить нам, что коллбэк может не обращать внимания на параметр `elapsedTime`, но для того, чтобы этого достичь, всегда можно создать коллбэк, который принимает меньшее число аргументов.

??? faq "16 (4). Как в TypeScript перегрузить конструктор класса"

    TypeScript позволяет объявлять множество вариантов методов, но реализация может быть лишь одна, и эта реализация должна иметь сигнатуру, совместимую со всеми вариантами перегруженных методов. Для перегрузки конструктора класса можно воспользоваться несколькими подходами:

    Можно воспользоваться необязательным параметром:

    ```ts
    class Box {
    public x: number
    public y: number
    public height: number
    public width: number

    constructor()
    constructor(obj: IBox)
    constructor(obj?: any) {
    	this.x = (obj && obj.x) || 0
    	this.y = (obj && obj.y) || 0
    	this.height = (obj && obj.height) || 0
    	this.width = (obj && obj.width) || 0
    }
    }
    ```

    Можно воспользоваться параметрами по умолчанию:

    ```ts
    class Box {
    public x: number
    public y: number
    public height: number
    public width: number

    constructor(obj: IBox = { x: 0, y: 0, height: 0, width: 0 }) {
    	this.x = obj.x
    	this.y = obj.y
    	this.height = obj.height
    	this.width = obj.width
    }
    }
    ```

    Можно использовать дополнительные перегрузки в виде методов статической фабрики:

    ```ts
    class Person {
    static fromData(data: PersonData) {
    	let { first, last, birthday, gender = 'M' } = data
    	return new this(`${last}, ${first}`, calculateAge(birthday), gender)
    }

    constructor(public fullName: string, public age: number, public gender: 'M' | 'F') {}
    }

    interface PersonData {
    first: string
    last: string
    birthday: string
    gender?: 'M' | 'F'
    }

    let personA = new Person('Doe, John', 31, 'M')
    let personB = Person.fromData({
    first: 'John',
    last: 'Doe',
    birthday: '10-09-1986'
    })
    ```

    Можно использовать тип-объединение:

    ```ts
    class foo {
    private _name: any
    constructor(name: string | number) {
    	this._name = name
    }
    }
    var f1 = new foo('bar')
    var f2 = new foo(1)
    ```

??? faq "17 (4). Чем различаются ключевые слова interface и type в TypeScript?"

    Вот примеры использования этих ключевых слов:

    ```ts
    interface X {
    a: number
    b: string
    }

    type X = {
    a: number
    b: string
    }
    ```

    В отличие от объявления интерфейса, которое всегда представляет именованный тип объекта, применение ключевого слова `type` позволяет задать псевдоним для любой разновидности типа, включая примитивные типы, типы-объединения и типы-пересечения.

    При использовании ключевого слова `type` вместо ключевого слова `interface` теряются следующие возможности:

    - Интерфейс может быть использован в выражении `extends` или `implements`, а псевдоним для литерала объектного типа — нет.
    - Интерфейс может иметь несколько объединённых объявлений, а при использовании ключевого слова `type` эта возможность не доступна.

??? faq "18 (5). Расскажите о том, когда в TypeScript используют ключевое слово declare"

    Ключевое слово `declare` используется в TypeScript для объявления переменных, источником которых может служить некий файл, не являющийся TypeScript-файлом.

    Например, представим, что у нас имеется библиотека, которая называется `myLibrary`. У неё нет файла с объявлениями типов TypeScript, у неё имеется лишь пространство имён `myLibrary` в глобальном пространстве имён. Если вы хотите использовать эту библиотеку в своём TS-коде, вы можете использовать следующую конструкцию:

    ```ts
    declare var myLibrary
    ```

    TypeScript назначит переменной `myLibrary` тип `any`. Проблема тут заключается в том, что у вас не будет, во время разработки, интеллектуальных подсказок по этой библиотеке, хотя использовать её в своём коде вы сможете. В этой ситуации можно воспользоваться и другим подходом, ведущим к тому же результату. Речь идёт об использовании переменной типа `any`:

    ```ts
    var myLibrary: any
    ```

    И в том и в другом случае при компиляции TS-кода в JavaScript, получится одно и то же, но вариант с использованием ключевого слова `declare` отличается лучшей читабельностью. Применение этого ключевого слова приводит к созданию так называемого внешнего объявления переменной (ambient declaration).

??? faq "19 (5). Что такое внешние объявления переменных в TypeScript и когда их нужно использовать?"

    Внешнее объявление переменной (ambient declaration) — это механизм, который позволяет сообщать компилятору TypeScript о том, что некий исходный код существует где-то за пределами текущего файла. Внешние объявления помогают интегрировать в TS-программы сторонние JavaScript-библиотеки.

    Эти объявления делают в файле объявления типов с расширением `.d.ts`. Внешние переменные или модули объявляют так:

    ```ts
    declare module Module_Name {}
    ```

    Файлы, в которых находится внешний код, должны быть подключены в TS-файле, использующем их, так:

    ```ts
    /// <reference path=" Sample.d.ts"></reference>
    ```

??? faq "20 (5). Можно ли автоматически генерировать файлы объявлений TypeScript из JS-библиотек?"

    JavaScript не всегда содержит достаточно информации, которая позволяет TypeScript автоматически выводить типы. Поэтому практически невозможно автоматически создавать объявления типов, основанные на JavaScript. Однако можно попытаться это сделать, воспользовавшись следующими инструментами:

    - Microsoft/dts-gen — официальное средство, используемое Microsoft как отправная точка при создании объявлений типов.
    - dtsmake — многообещающий инструмент для автоматического создания объявлений типов на основе JS-файлов, находящийся в процессе разработки. Он зависит от системы анализа кода Tern, которую используют некоторые редакторы для реализации механизма автозавершения при вводе JS-кода.

## Ссылки

- [20 вопросов и ответов](https://habr.com/ru/company/ruvds/blog/419993/)
