---
description: Требуется породить выходную последовательность из входной, причем каждый элемент выходной последовательности может быть произвольно сложной функцией от входных данных и размеры последовательностей не обязательно совпадают
---

# Исключение рекурсии с помощью выражений for

## Задача

Требуется породить выходную последовательность из входной, причем каждый элемент выходной последовательности может быть произвольно сложной функцией от входных данных и размеры последовательностей не обязательно совпадают.

## Решение

### XPath 1.0

К версии 1.0 неприменимо. Необходимо использовать рекурсивный XSLT-шаблон.

### XPath 2.0

Воспользуемся выражением `for`. В следующих примерах показано, как с помощью этого выражения можно отображать одну последовательность на другую, причем их размеры могут отличаться.

#### Агрегирование

Сумма квадратов: `sum(for $x in $numbers return $x * $x)`

Усреднение квадратов: `avg(for $x in $numbers return $x * $x)`

#### Отображение

Отобразить последовательность слов во всех абзацах на последовательность длин слов: `for $x in //para/tokenize(.,' ') return string-length($x)`

Отобразить последовательность слов в абзаце на последовательность их длин, но только для слов, содержащих более 3 букв: `for $x in //para/tokenize(.,' ') return if (string-length($x) gt 3) then string-length(\$x) else ()`

То же самое, но с условием на входную последовательность: `for $x in //para/tokenize(.,' ')[string-length(.) gt 3] return string-length($x)`

#### Порождение

Породить последовательность квадратов первых 100 целых чисел: `for $i in 1 to 100 return $i _ $i`

Породить последовательность квадратов в обратном порядке: `for $i in 1 to 10 return (10 - \$i) _ (10 - \$i)`

#### Расширение

Отобразить последовательность абзацев на последовательность, в которой каждый абзац повторяется дважды: `for $i in //para return ($x, $x)`

Продублировать слова: `for $x in //para/tokenize(.,' ') return ($x, $x)`

Сопоставить каждому слову это же слово, за которым следует его длина: `for $x in //para/tokenize(.,' ') return ($x, string-length(\$x))`

#### Соединение

Для каждого клиента вывести идентификатор и общую сумму по всем его заказам:

```
for $cust in doc('customer.xml')/*/customer
return
   ($cust/id/text(),
sum(for $ord in (doc('orders.xml')/*/order[custID eq $cust/id]
return ($ord/total)) )
```

## Обсуждение

Добавление конструкций для управления потоком выполнения программы в язык выражений может поначалу показаться странным, а то и ошибочным решением. Но по мере овладения всей мощью XPath 2.0 эти сомнения отпадут. Особенно это относится к выражению `for`. Достоинства выражения `for` становятся очевидны, когда вы понимаете, как с его помощью можно упростить многие рекурсивные решения, характерные для XSLT 1.0.

Рассмотрим задачу вычисления сумм в XSLT 1.0. Если вам нужно вычислить простую сумму значений, то проблемы не возникает, так как в XSLT 1.0 есть встроенная функция `sum`. Но уже для вычисления суммы квадратов приходится писать более громоздкий и не сразу понятный рекурсивный шаблон. Вообщето, значительная часть рецептов в первом издании этой книги как раз и была посвящена готовым решениям таких упражнений на применение рекурсии. При наличии XPath 2.0 сумма квадратов вычисляется проще пареной репы:

```
sum(for $x in $numbers return $x \* $x)
```

, где `$numbers` – исходная последовательность чисел. Подумайте, сколько деревьев я мог бы сохранить, если
бы такая возможность существовала в XPath 1.0!

Однако этим мощь выражения `for` не исчерпывается. Итерировать можно не только по одной переменной. С помощью нескольких переменных можно организовывать вложенные циклы для порождения последовательностей из взаимосвязанных узлов сложного документа.

Возвращает последовательность, содержащую идентификаторы абзацев и идентификаторы тех абзацев, на которые имеются ссылки:

```
for $s in /*/section,
 $p in $s/para,
 $r in $p/ref
return ($p/@id, $r)
```

Вы должны понимать, что семантически это выражение эквивалентно следующему, хотя и более компактно:

```
for $s in /\*/section
return $p in $s/para
return for $r in $p/ref
return ($p/@id, $r)
```

Заметим также, что необязательно использовать вложенные выражения `for`, когда порождаемую последовательность можно более элегантно представить с помощью традиционного путевого выражения.

Это нагромождение `for` – всего лишь многословный эквивалент выражения `/_/section/para/ref`:

```
for \$s in /_/section,
$p in $s/para,
$r in $p/ref return \$r
```

Иногда возникает необходимость узнать позицию каждого обрабатываемого элемента в последовательности. Воспользоваться для этого функцией `position()`, как в конструкции `for-each`, не получится, поскольку при вычислении выражения `for` в XPath позиция контекстного узла не изменяется. Но того же результата можно достичь следующим образом:

```
for $pos in 1 to count($sequence),
$item in $sequence[$pos]
return $item, $pos
```
