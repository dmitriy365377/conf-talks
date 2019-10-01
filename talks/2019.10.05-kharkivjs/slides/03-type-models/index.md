# Type Models

-----

## Основа в `Type Models` это генерация моделей из схемы, которую предоставил вам сервер.

-----

## Частенько такой же подход используется со Swagger'ом в REST API.

-----

### Получили описание серверного типа:

```graphql
type Image {
  url: URL!
  width: Int!
}

```

### Сгенерировали модель со всеми полями:

```typescript
interface ImageModel {
  getUrl(): URL;
  getWidth(): number;
}

```

Генерация кода спасет мир! ❤️ <!-- .element: class="green fragment" -->

-----

## Опечатки пропадают <br/>и с типизацией становится всё нормально <!-- .element: class="green" -->

-----

## Но куда же без проблем <!-- .element: class="red" -->

-----

### Проблема 2.1: Алиасы в GraphQL-запросе

```graphql
fragment SquareImage on HasImage {
  smallPic: image(width: 40) {
    url
  }
  bigPic: image(width: 400) {
    url
  }
}

```

<span class="fragment">Поле `image` будет сгенерировано из серверной схемы.</span>

<span class="fragment">А вот `smallPic` или `bigPic` придется ручками в модель добавлять. Опять черевато ошибками!</span>

-----

### Проблема 2.2: Масштабирование

### <br/>В Фейсбуке приблизительно <!-- .element: class="orange" -->

- ~30'000 типов
- ~200'000 полей

-----

## Представьте сколько классов и геттеров сгененрируется на базе серверной схемы! ☝️ <!-- .element: class="orange" -->

-----
Что теперь весь сгененрированный код надо включать во все приложения и клиенты, которые могу использовать только сотую часть от всей схемы?! Это ужасно неоптимально. Чистить руками сгенерированный код, тоже не шибко интересная затея.

#### Вывод по Type Models

- ~~Опечатки (typos)~~
- ~~Отсутствие типовой безопасности (type safety)~~
- Недополучения данных (underfetch)
- Получение лишних данных (overfetch)
- Возможна куча сгенерированного кода

Генерация моделей из серверной схемы спасает от опечаток (typos) и отсутствия типовой безопасности (type safety).

Но проблема underfetch сохраняется: Если вы не запросили поле в запросе, то вы все равно сможете ошибочно вызвать это поле в вашей компоненте и нарваться на грех в рантайме (cannot read property of null, null pointer exception).

И проблема overfetch тоже никуда не девается: например вы упростили компоненту, перестав использовать какое-то поле и вдруг забыли удалить его в GraphQL-запросе, то вы будете тянуть данные ненужного поля на клиент. Ок, вы можете быть супер ответственным и удалить это поле и в запросе, но бац и приложение упало с проблемой `underfetch` – оказывается кто-то данные этого поля использует в другой части приложения. Т.е. если я удалил поле, то я должен пробежаться по всему приложению, чтобы убедиться в том, что его больше никто не использует.

Проблемы:

- Когда много команд
  - Все команды шарят между собой одну гигантскую библиотеку моделей типов
  - ИЛИ нет переиспользуемых компонентов/запросов между командами
  - ИЛИ разбивка на "собственные болота"
    - выбор верного болота или создавай свое
- Билды приложения могу ломаться, если другие команды удаляют поля из GraphQL-запросов