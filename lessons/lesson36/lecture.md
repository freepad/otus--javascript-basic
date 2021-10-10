---
title: Занятие 36
description: «Публикация проектов - github, npm»
---

# OTUS

## Javascript Basic

<!-- v -->

## Публикация проектов - npm, github

<!-- v -->

### План вебинара:

- NPM
- пакеты и модули
- практика публикации пакета на npm
- github workflow

<!-- s -->

# NPM

<!-- v -->

### NPM - CLI (Command-line interface/input)

- npm init
- npm install
- npm uninstall
- ...

<!-- v -->

### NPM - Хранилище/реестр ([registry](https://registry.npmjs.org))

<!-- v -->

### NPM - Коммьюнити

npm <3 это мы

<!-- v -->

### NPM - [Веб-сайт](https://www.npmjs.com/)

<!-- v -->

### NPM - Компания (npm, Inc)

<!-- v -->

## Пакеты и модули

<!-- v -->

### Пакет

Файл или директория, описываемая с помощью **package.json**

<!-- v -->

### Форматы пакетов

- (a) `папка`, содержащая программу, описанную в package.json
- (b) `gzipped tar aрхив`, содержащий (a).
- (с) `URL адрес`, ведущий к (b).
- (d) **`<name>@<version>`** опубликованное в реестре с (c).
- (e) **`<name>@<tag>`** указывающая на (d).
- (f) **`<name>`** c тэгом **latest**, удовлетворяющем (e).
- (g) `git адрес`, который, будучи cклонированным, является (a).

<!-- v -->

### Git URL форматы пакетов

- git://github.com/user/project.git#commit-ish
- git+ssh://user@hostname:project.git#commit-ish
- git+http://user@hostname/project/blah.git#commit-ish
- git+https://user@hostname/project/blah.git#commit-ish

где **commit-ish** - тэг, хэш или любой аргумент принимаемый **git checkout**  
значение по умолчанию для commit-ish - **master**

<!-- v -->

### Модуль

Файл или директория в **node_modules**, который может быть загружен с помощью Node.js функции **require()**

<!-- v -->

### Модулем может являться:

- директория с package.json, содержащей поле **"main"**
- JavaScript файл

**так как для модуля не является необходимым наличие package.json, модуль - это не всегда пакет!**

<!-- v -->

## Пространства имён (scopes)

При регистрации npm аккаунта каждому пользователю автоматически предоставляется определённый **scope** или **пространство имён**, совпадающие с **именем** пользователя, используемое для связанных с ним пакетов

**@username**/package-name

<!-- v -->

### Пространства имён и уровни доступа

- пакеты вне пространства имён всегда публичные
- приватные пакеты всегда находятся в пространстве имён
- пакеты в пространстве имён являются приватными по умолчанию

чтобы изменить уровень доступа пакета в пространстве имён с приватного на публичный нужно использовать специальный флаг при его публикации с помощью CLI

**npm publish** _--access public_

<!-- v -->

### package.json

- отображает список пакетов необходимых для проекта
- определяет версии пакетов, от которых зависит проект используя **семвер** (семантическое версионирование)
- позволяет вашему билду быть репродуцируемым (воспроизводимым), тем самым простым для совместного использования разработчиками
- отражает другую полезную мета-информацию

<!-- v -->

### Поля package.json

**Обязательные:**

- **name** - содержит имя пакета, должно начинаться со строчной буквы и являться одним словом, может содержать тире и нижние подчёркивания
- **version** - должно быть в форме **x.x.x** согласно семвер

Дополнительные:

- _author_ - имя разработчика
- _description_ - описание проекта
- _keywords_ - ключевые слова, с помощью которых пользователи могут найти ваш пакет в реестре с помощью **npm search**
- _license_ - лицензия
- _workspaces_ - список путей к рабочему пространству системы (**npm v7** и выше)
- ...

<!-- v -->

### Особые поля при работе с пакетами

- **main** - ID модуля, который является входной точкой программы. В случае когда пользователь устанавливает его и делает **require('имя_модуля')** экспортируемый объект из модуля будет возвращён. Значение по умолчанию **index.js**. **!!!Необходимо для корректной работы модуля**
- **files** - массив, представляющий собой набор паттернов, описывающих пути к файлам, необходимым для включения в пакет. **package.json** будет включён в пакет, независимо от наличия в files!
- **private** - значение этого поля `true` отключает возможность npm публиковать пакет

<!-- v -->

### Инициализация package.json

**npm init**  
**npm init** _--scope=@my-username_  
**npm init** _--yes_

переопределение свойств используемых по умолчанию

<!-- eslint-skip -->

```js
> npm set init.author.email "example-user@example.com"
> npm set init.author.name "example_user"
> npm set init.license "MIT"
```

<!-- v -->

### Публикация пакета

**npm publish**

!!!Строго рекомендуется убирать важную информацию, такую как: пароли, приватные ключи и т.д.

**.gitignore**  
**.npmignore**

<!-- v -->

### Хранилища/реестры

- [npm](https://registry.npmjs.org)
- [github](https://github.com/features/packages)
- [docker](https://docs.docker.com/registry/)
- ...

**npm config set registry** *https://registry.your-registry.npme.io/*  
файл [.npmrc](https://docs.npmjs.com/configuring-your-registry-settings-as-an-npm-enterprise-user)

<!-- v -->

### Установка пакета

**npm install** _my-package_  
**npm install** _@username/my-package_

**npm install** _--production_

Установка пакетов из списка зависимостей **транзитивна**, если _`package<A>`_ устанавливается с помощью **npm install** и у него есть в зависимостях _`package<B>`_, то он также будет установлен вместе со своими зависимостями

<!-- v -->

### Удаление пакета

**npm uninstall** _my-package_  
**npm uninstall** _@username/my-package_

<!-- v -->

### Семантическое версионирование

- **МАЖОРНАЯ версия 2.x.x**, когда сделаны обратно несовместимые изменения API.
- **МИНОРНАЯ версия x.1.x**, когда вы добавляете новую функциональность, не нарушая обратной совместимости.
- **ПАТЧ-версия x.x.1**, когда вы делаете обратно совместимые исправления.

<!-- v -->

### Спецсимволы

- **`~`** - обновление патч-версии с исходной минорной **`1.1.x`** _(если минорная версия не указана, разрешены обновления с исходной мажорной **`1.x.x`**)_
- **`^`** - обновление минорной версии с исходной мажорной **`1.x.x`**
- **`*`** - любая версия
- **`latest`** - последний релиз

[npm semver calculator](https://semver.npmjs.com/)

<!-- v -->

### Обновление версии пакета

**npm version** [ _`<newversion> | major | minor | patch | premajor | preminor...`_ ]  
**npm publish**

<!-- v -->

### Дистрибутивные теги

Человекочитаемые метки, которые помогают организовать и пометить разные версии публикуемого пакета. Являются своеобразным дополнением к **семвер**

**npm publish** _`--tag <tag>`_  
npm publish --tag beta

**npm dist-tag add** _`<package-name>@<version> [<tag>]`_  
npm dist-tag add example-package@1.4.0 stable

<!-- v -->

### README

Для улучшения пользовательского опыта работы с вашим пакетом и его быстрого поиска в реестре, рекомендуется создать в корневой директории **README.md**.

<ins>В него можно включить</ins>:

- _описание вашего пакета, его изменений и обновлений_
- _конфигурацию_
- _способы использования_
- _другую полезную для пользователя информацию_

<!-- v -->

### Прекращение поддержки

**npm deprecate** _`<package-name> "<message>"`_  
**npm deprecate** _`<package-name>@<version> "<message>"`_

<!-- v -->

### Депубликация пакета

**npm unpublish** _`<package-name>@<version>`_  
**npm unpublish** _`<package-name> -f`_

<!-- v -->

## Вопросы?

<!-- s -->

## Практика

### Создаём и публикуем свой пакет!

<!-- v -->

## Github Workflow

### для публикации своего пакета на npm

<!-- v -->

## Материалы

- [пакеты и модули](https://docs.npmjs.com/packages-and-modules)
- [поля package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)
- [npm команды](https://docs.npmjs.com/cli/v7/commands)
- [семвер npm](https://docs.npmjs.com/about-semantic-versioning)

<!-- v -->

### Домашнее задание

Покрыть тестами и опубликовать свою реализацию redux

1. в репозитории прошлого проекта создать новую ветку
2. добавить поддержку applyMiddleware
3. покрыть код тестами
4. опубликовать пакет
5. создать новый проект, и за использовать в нем опубликованный пакет (достаточно базовых операций по созданию store, диспатчу пару actions и проверке state)

<!-- v -->

6. опубликовать тестовый проект
7. выложить ссылку на свой пуллреквест выложить в общий чат
8. сделать **2** ревью в чужих пуллреквестах
9. получить **2** ревью в своем пуллреквесте
10. при найденных багах - создать issues в чужих репозиториях
11. покрыть тестами и исправить баги найденные другими студентами
12. ссылку на тестовый проект (на код, и на опубликованную страницу) и на пуллреквест сбросить в чат с преподавателем

<!-- v -->

### Критерии оценки

- есть поддержка applyMiddleware - **3** балла
- опубликован пакет - **1** балл
- есть тестовый проект для проверки пакета - **1** балл
- сделано ревью 2 PR - **1** балл
- получено 2 ревью - **1** балл
- создано issue в чужом репозитории - **1** балл за issue (не больше **2**)
- исправлены issues в своем репозитории (тесты + фикс) - **1** балл за issue (не больше **4**)

**Принято - от 9 баллов**

<!-- v -->

## Спасибо за внимание!