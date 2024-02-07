# 8. Домашнее задание к занятию "Объектно-ориентированное программирование: ключевые принципы"

## Цель задания

1. Научиться проектировать объекты для хранения данных

------

## Инструкция к заданию

1. Скачайте и установите профессиональный редактор кода [Intellij Idea Community Version](https://www.jetbrains.com/idea/download/)
1. Откройте IDEA и [создайте и настройте новый Maven-проект](QA_Maven_Idea_Create.md) (под каждую задачу следует создавать отдельный проект, если обратное не сказано в условии)
2. Создайте пустой репозиторий на GitHub и свяжите его с папкой вашего проекта (не с какой-либо другой папкой).
3. Правильно настройте репозиторий в плане `.gitignore`. Проигнорируйте папки `.idea` и `target` (раньше была `out`) и `.iml`-файл - их в репозитории быть не должно.
4. В этом задании настраивать CI не требуется
5. Выполните в IDEA требуемую задачу согласно условию.
6. Проверьте соблюдение [правил форматирования кода](QA_Java_Idea_Format.md)
7. Закоммитьте и отправьте в репозиторий содержимое папки проекта.

------

## Материалы, которые пригодятся для выполнения задания

1. [Как создать Maven-проект в IDEA?](QA_Maven_Idea_Create.md)
1. [Как отформатировать код в Java?](QA_Java_Idea_Format.md)

------

## Задание 1 (обязательное)

В этой задаче, в отличие от всех последующих, настраивать CI не требуется.

Вспомните [условие задачи](https://github.com/netology-code/iqa-homeworks/tree/iqa-12/2.4#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2) из курса по ручному тестированию, где вы общались с сервером. Тогда на сервер вы посылали информацию в виде JSON — текстового формата описания объекта в JavaScript-стиле, выглядела она так:
```json
{
  "birthday": "13.06.1999",
  "name": "Иван",
  "passport": "4444 № 44444444",
  "patronymic": "Иванович",
  "phone": "+7 (999)-999-99-99",
  "surname": "Иванов"
}
```

Немного усложним и добавим в неё ещё информацию о том, согласен ли пользователь получать новости о скидках в виде sms: `"subscription": true`. Также предлагается, чтобы дата рождения была не полем-строкой, а тоже объектом: `"birthday": {"day" : 13, "month": 6, "year": 1999}`. В итоге объект в запросе будет выглядеть, например, так:

```json
{
  "birthday": {
    "day": 13,
    "month": 6,
    "year": 1999
  },
  "name": "Иван",
  "passport": "4444 № 44444444",
  "patronymic": "Иванович",
  "phone": "+7 (999)-999-99-99",
  "surname": "Иванов",
  "subscription": true
}
```

Вашей задачей будет разработать классы, описывающие объекты запроса анкеты на сервер, и продемонстрировать их работу в `Main`.

Создайте класс `Post`, описывающий объект запроса на сервер, и заполните его полями. Сперва можно без `birthday`, так как для него придётся создавать вспомогательный класс, выбрав подходящие типы:
```java
public class Post {
  public String name; // поле для имени
  // добавьте другие поля
}
```

Создадим класс `Main`, в `main` которого создадим и заполним наш объект:
```java
public class Main {
    public static void main(String[] args) {
        Post post = new Post();
        post.name = "Иван";
        // заполните другие поля
    }
}
```

Поставим точку останова на последней строчке, можно прямо на закрывающей фигурной скобке `main`, и запустим отладчик, чтобы посмотреть, что у нас будет лежать в переменной с объектом:

![image](https://user-images.githubusercontent.com/53707586/212560750-3a50d752-f62d-4554-84bf-4a81bea4bad7.png)




Если вы сделали всё правильно, то в отладчике будет виден созданный и заполненный объект типа `Post` по схеме данных — полей — указанных вами в классе `Post`.

Осталось добавить поле `birthday`. Значение в этом поле должно быть объектом, для которого также нужно будет создать свой класс. Создайте класс `FormDate` для описания схемы объекта в поле `birthday`:
```java
public class FormDate {
  // добавьте три необходимых поля
}
```

Теперь в классе `Post` добавьте поле `birthday` с типом `FormDate`. После чего добавьте заполнение этого поля в `main`:
```java
  post.birthday = new FormDate();
  post.birthday.day = 13;
  // заполните другие поля даты рождения
```

Запустите отладчик снова и убедитесь, что всё заполнено как надо и соответствует JSON-описанию объекта выше.

------

## Правила приема работы

Прикреплена одна ссылка на публичный репозиторий с решением задачи.

------

## Критерии оценки

1. В каждом репозитории размещено содержимое папки проекта IDEA. Корнем репозитория должна именно папка проекта - не папка `src`, не папка внутри которой лежит папка проекта; т.о. в корне репозитория должна лежать сразу папка `src`.
1. Есть файл `.gitignore`, игнорирующий ненужные файлы и папки, которые должны отсутствовать в репозитории. Если они присутствуют - их нужно оттуда удалить.
1. Программа соответствует всем требованиям из условия задачи
1. Программа использует только те инструменты языка, которые мы проходили или которые прямо разрешены условием задачи
1. Программа работает правильно на всех примерах из условия
1. Программный код отформатирован и соответствует пройденным требованиям к качеству кода
1. Программа спроектирована достаточно логично и правильно, не противоречит общепринятым в производстве практикам и традициям
1. При наличии недочётов, в зависимости от их серьёзности и количества, работа может быть отправлена на доработку или принята; решение принимается на основе экспертной оценки работы.