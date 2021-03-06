# Создаем свой GraphQL-сервер на NodeJS

## Слайды: [тёмная тема](https://nodkz.github.io/conf-talks/talks/2020.04.07-workshop-graphql-on-server/index.html) или [светлая тема](https://nodkz.github.io/conf-talks/talks/2020.04.07-workshop-graphql-on-server/white.html)

Workshop может дать существенный толчок в изучении GraphQL начинающим специалистам. А так же заинтересовать и опытных специалистов. Вас ждет много интересного материала простым и доступным языком.

По окончании воркшопа у группы должно сложиться понимание из каких частей состоит GraphQL-сервер, как он работает, как конструировать схемы, с какими проблемами придется столкнуться и как их необходимо решать.

Воркшоп проводят:
- Павел Черторогов – один из ведущих специалистов по GraphQL, который работает с ним больше 4-х лет и сделал более 15 докладов о данной технологии.
- Алексей Золотых – teamlead Infobip, член программного коммитета HolyJS, спикер и самый крупный фронтендер.

## GraphQL на сервере (программа воркшопа 1го дня):

### 1) Знакомство с GraphQL

- Чем хорош GraphQL и почему он стал таким популярным?
- Что такое GraphQL-сервер?
- Что такое GraphQL-схема и из каких примитивов она состоит?
  - основные типы Scalar, Object, Input, Enum
  - модификаторы NonNull, List
  - как написать кастомный скаляр
  - Interfaces и Unions
  - Directives
- Какие операции есть в GraphQL и как они отличаются друг от друга?
  - query
  - mutation
  - subscription
- Что такое контекст и как он работает?
- Подходы к построению схем
  - schema-first
  - code-first
  - генерация схем
- Дизайн GraphQL-схем
  - почему схема по умолчанию nullable
  - популярные принципы и лайфхаки в построении схем

### 2) Создаем GraphQL-схему

- Подходы в построении схем
  - graphql-js
  - graphql-tools
  - graphql-compose
  - type-graphql
  - nexus
  - graphql modules
  - graphql-compose-modules
  - NestJS
- Написание Entity (Order)
  - создание Query
- Написание второй Entity (Employee)
  - связь между типами
- Изменяем данные через Mutation
- Реализуем Subscription
  - Как работают Subscriptions под капотом

### 3) Решаем стандартные проблемы

- N+1 Problem
- Query cost
- Авторизация (cookies, заголовки)
- Логирование (Winston)
- Отлов ошибок (Sentry)
- Трассировка (Elastic APM)

### 4) Обсуждения разных тем (зависит от оставшегося времени, и от интереса присутствующих):

- Несколько схем на одном сервере (админская, пользовательская)
- Версионирование GraphQL-схем
- Производительность GraphQL
- Как прикрутить GraphQL к существующему REST API
- Микросервисная архитектура: schema-stiching, Apollo Federation
  - [How to GraphQL in Kotlin and create a single endpoint to access microservices' APIs](https://romankudryashov.com/blog/2020/02/how-to-graphql/)
