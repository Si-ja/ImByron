# ImByron

## Описание

ImByron / ЯБайрон это маленкий проект, который я хотел сделать с использованием родного языка и в контексте Data Science.

Идея проекта заключается в том, чтобы создать алгоритм, который используя метод "Цепей Маркова" мог бы на основе "оригинальных" (переведённые) поэм Байрон (Джордж Гордон) генерировать новые поэмы.

Вышеупомянутая основная идея разбита на несколько дополнительных компонентов:

1. Создание алгоритма, который может скачать из онлайн ресурса стихи Байрона, которые бы могли использоваться для генерации новых стихов.
2. Создание вебсайта с описанием для проекта, и генератором новых стихов.
3. Создание генератора, встроенного в API на вебсайте.

## Основные Шаги

### Инструменты

Для выполнения всех шагов использовались следующие ресурсы или инструменты: 
* Python 3
* Jupyter Notebook
* HTML
* CSS
* Bootstrap
* JQuery
* Markdown
* https://rustih.ru/dzhordzh-bajron/

### Скачивание стихов.

Стихи были скачены из онлайн ресурса: https://rustih.ru/dzhordzh-bajron/. Алгоритм, который был создан для скачивания стихов, создан таким образом, чтобы в дальнейшем его можно было пере-использовать и для скачивания работ других писателей\поэтов на упомянутом ресурсе.

Чтобы не перезагружать сайт запросами - между скачиванием каждого последующего стиха, добавлена следующая команда:

```python
rng = random.randint(4, 8)
time.sleep(rng)
```
Она отвечает за то, чтобы случайным образом делалась пауза от 4 до 8 секунд, между каждым последующим запросом, высланным на сайт РуСтих. Таким образом, идёт попытка уменьшить нагрузку на вебсайт и добиться того чтобы каждый запрос был приблизительно близок к той скорости, с которой бы стихи скачивал, копируя их, обычный пользователь.

Сам алгоритм находится в файле `GetLyrics.ipynb` Скаченный и "очищенный" текст поэм на ГитХаб ресурсе с самим проектом не указан.

Заметка: Стихи использованы для данного проекта только в целях обучения.

### Создание вебсайта.

Так как большая часть моих навыков это back-end, а не графический дизайн и оформление, а тем более веб-дизайн, задача была поставлена создать вебсайт используя Python 3 и Bootstrap.

Python 3 и модуль Flask позволяют создать "скелет" для вебсайта максимально быстро, так чтобы все запросы пользователя обрабатывались через Python, а не через какую-нибудь версию\форму JavaScript. При использовании заготовленных компонентов от Bootstrap, создание вебсайта требует минимальной работы с HTML и CSS. JQuery использовался только для того чтобы передавать информацию от пользователя в алгоритмы сделанные в Python 3.

Для вебсайта были созданы 2 страницы: Основной генератор и краткое описание того на основе какой модели генерируются новые стихи (данное описание указано в конце этого файла).

Главная страница:
![](https://github.com/Si-ja/ImByron/blob/master/VisualExamples/MainPage_Clean.PNG?raw=true "CleanMainPage")

Главная страница + сгенерированный стих
![](https://github.com/Si-ja/ImByron/blob/master/VisualExamples/MainPage_Example.PNG?raw=true "PopulatedMainPage")

Описание:

![](https://github.com/Si-ja/ImByron/blob/master/VisualExamples/DescriptionPage_1.PNG?raw=true "DescriptionPage_1")
![](https://github.com/Si-ja/ImByron/blob/master/VisualExamples/DescriptionPage_2.PNG?raw=true "DescriptionPage_2")

### API

Разработка API добавлена была для того, чтобы пользователю не требовалось посещать вебсайт, чтобы сгенерировать новый стих. К сожалению, потому что все стихи сгенерированы используя кириллицу - информация на выходе не читается правильно, и кодировка букв нарушается. Для того чтобы прочесть текст - можно скопировать его содержание и использовать конвертер (https://www.online-toolz.com/tools/text-unicode-entities-convertor.php) как в данном примере: 

API на вебсайте: 
![](https://github.com/Si-ja/ImByron/blob/master/VisualExamples/APIExample.PNG?raw=true "WEB_API")

API в командной строке:
![](https://github.com/Si-ja/ImByron/blob/master/VisualExamples/curl_example.PNG?raw=true "curl_API")

Онлайн конвертер:
![](https://github.com/Si-ja/ImByron/blob/master/VisualExamples/WorkingConverter.PNG?raw=true "Converter_Example")

### Итог:

В этом проекте помимо того, что я хотел вернуться к работе с Python, я так же хотел научиться вещам, с которыми никогда не работал:

* Создание API
* Использование Bootstrap
* Проект на русском языке

Всё по большей мере сделано для души и ради интереса (например мне довелось почитать вновь стихи Байрона, которые мне нравятся) и поделиться проектом, который может кому-то принесёт пользу.

### П.С. информация из описания проекта:

Приложение по генерации новых словосочетаний, которые потенциально могут быть сложены во что-то что мог бы написать Байрон. Принцип работы построен на основе "Цепей Маркова".

Достаточно часто сгенерированные стихи совершенно не будут похожи даже на что-то что мог бы написать рациональный человек. Это связано с тем, что генерация новых словосочетаний, используя метод "Цепей Маркова", является частично случайной и создание новых слова в последовательности зависит от того, какие слова использовались ранее. Например, при параметре "порядка" равным 2, первые два слова стиха выбираются абсолютно случайно из всех возможных комбинаций слов, которые когда-либо присутствовали в работах поэта. Далее, алгоритм берёт случайно выбранные ранее слова, и создаёт список всех комбинаций в которых использовались именно 2 предыдущих слова и оценивает какое слово может идти за ними. Например, если первые два слова были "я" и "хочу", то третьим могут быть такие слова как "быть", "увидеть", "понять" и т.д. Тогда, алгоритм случайным образом выбирает одну из этих комбинации и третье слово из неё добавляет в генерируемую поэму, например, "быть". Далее процесс повторяется, только теперь алгоритм оценивает все комбинации слов, которые имеют последовательность "хочу быть". Увеличивая параметр "порядка", алгоритм будет оценивать комбинацию уже не двух слов, а более. Качество новых генераций растёт, когда объём информации велик. В таких случаях выбор различных словосочетаний становится больше. Параметр "порядка" можно увеличивать, что должно вести к созданию более похожей человеческой речи в письме. К сожалению, у данного поэта только 113 поэм и многие из них переведены разными писателями, а это значит, что стилистика не постоянна и потому количество существующих комбинации уменьшается. Малый объём информации так же означает, что увеличивать переменную "порядка" это проблематично, так как в таком случаи количество существующих комбинации будет мало, и алгоритм будет генерировать уже существующие стихи, ибо только в них может присутствовать та комбинация слов, которую алгоритм нашёл. Но даже при всём этом, алгоритм полностью игнорирует наличие знаков препинаний в работах поэта, поэтому они добавлены на основе нескольких правил и могут быть совершенно не подходящими для реального использования.

Нам самом деле - использование такой методологии — это только концепция. Воссоздание настоящей человеческой речи, при том и в поэзии и с определённой стилистикой - это очень не лёгкое задание для машин. Цель этого проекта была создать в Python 3 алгоритм который может собрать определённую информацию из интернета, обработать её, и потом использую "Цепи Маркова" произвести что-то новое. После чего, создать рабочую среду для пользователя, который мог бы взаимодействовать с созданным кодам, при условии, что вся эта среда сделана использую ресурсы Bootstrap. Проект сделан только ради образования, и не будет использоваться в коммерческих целях. Так же, база данных со стихами Байрона была обработана, таким образом, что стихи потеряли структуру, и любые знаки препинания. Таким образом, для других целей помимо этого проекта они не могут быть использованы практический и не ничего не забирают от оригинального источника.
