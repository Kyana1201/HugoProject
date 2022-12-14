---
title: Управление версиями
subtitle: GIT — распределённая система управления версиями, созданная Линусом Торвальдсом для управления разработкой ядра Linux и в настоящее время получившая очень широкое распространение в среде разработчиков программного обеспечения.

# Summary for listings and search engines
summary: GIT — распределённая система управления версиями, созданная Линусом Торвальдсом для управления разработкой ядра Linux и в настоящее время получившая очень широкое распространение в среде разработчиков программного обеспечения.

# Link this post with a project
projects: []

# Date published
date: '2022-10-08T00:00:00Z'

# Date updated
lastmod: '2022-10-08T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Academic

categories:
  - Demo
---

## Git — это распределённая система версий 

Системы контроля версий бывают локальными, централизованными или распределёнными.

 * Локальная система хранит файлы на одном устройстве, централизованная использует общий сервер, а распределённая — общее облачное хранилище и локальные устройства участников команды. В локальной системе удобно работать с большими проектами, но сложно взаимодействовать с удалённой командой.
 * В централизованной системе налажена удалённая работа, но всё привязано к одному серверу. Любой сбой или взлом может повредить файлы проекта.
 * В распределённой системе налажена удалённая работа. Если с файлами основного репозитория что-то случится — проект легко восстановить из копии любого участника команды.

## Git — это не GitHub
 **Git** — это программа, которую нужно установить и подключить к проекту для управления системой контроля версий. GitHub — это сайт-хранилище для историй версий проектов: вы подключаете Git, регистрируетесь на GitHub, создаёте онлайн-репозиторий и переносите файлы с Git на GitHub.

 **Git** — это самая популярная система контроля версий, а GitHub — онлайн-хранилище кода. Git и GitHub настроены на взаимодействие и поэтому часто используются как единый механизм работы с проектом.

 Если нужно, Git можно заменить альтернативной программой контроля версий, а GitHub — другим онлайн-хранилищем кода. Большинству работодателей это не нужно, поскольку знакомство с другими сервисами отнимает время и неудобно многим разработчикам.

## Основные команды git

#### Наиболее часто используемые команды git:

1. создание основного дерева репозитория:

   * git init

2. получение обновлений (изменений) текущего дерева из центрального репозитория:

   * git pull

3. отправка всех произведённых изменений локального дерева в центральный репозиторий:

   * git push

###  Процесс работы с Gitflow:
 #### Основные ветки (master) и ветки разработки (develop)

 Для фиксации истории проекта в рамках этого процесса вместо одной ветки master используются две ветки. В ветке master хранится официальная история релиза, а ветка develop предназначена для объединения всех функций. Кроме того, для удобства рекомендуется присваивать всем коммитам в ветке master номер версии. При использовании библиотеки расширений git-flow нужно инициализировать структуру в существующем репозитории:

  * git flow init

Для github параметр Version tag prefix следует установить в v.
После этого проверьте, на какой ветке Вы находитесь:

  * git branch


### Функциональные ветки (feature)

Под каждую новую функцию должна быть отведена собственная ветка, которую можно отправлять в центральный репозиторий для создания резервной копии или совместной работы команды. Ветки feature создаются не на основе master, а на основе develop. Когда работа над функцией завершается, соответствующая ветка сливается обратно с веткой develop. Функции не следует отправлять напрямую в ветку master.
Как правило, ветки feature создаются на основе последней ветки develop.

**Создание функциональной ветки** Создадим новую функциональную ветку:

   * git flow feature start feature_branch

**Окончание работы с функциональной веткой** По завершении работы над функцией
следует объединить ветку feature_branch с develop:

   * git flow feature finish feature_branch

### Ветки выпуска (release)
Когда в ветке develop оказывается достаточно функций для выпуска, из ветки develop создаётся ветка release. Создание этой ветки запускает следующий цикл выпуска, и с этого момента новые функции добавить больше нельзя — допускается лишь отладка, создание документации и решение других задач. Когда подготовка релиза завершается, ветка release сливается с master и ей присваивается номер версии. После нужно выполнить слияние с веткой develop, в которой с момента создания ветки релиза могли возникнуть изменения.
Благодаря тому, что для подготовки выпусков используется специальная ветка, одна команда может дорабатывать текущий выпуск, в то время как другая команда продолжает работу над функциями для следующего.
Создать новую ветку release можно с помощью следующей команды:

   * git flow release start 1.0.0

Для завершения работы на ветке release используются следующие команды:

   * git flow release finish 1.0.0

 ### Ветки исправления (hotfix)

Ветки поддержки или ветки hotfix используются для быстрого внесения исправлений в рабочие релизы. Они создаются от ветки master. Это единственная ветка, которая должна быть создана непосредственно от master. Как только исправление завершено, ветку следует объединить с master и develop. Ветка master должна быть помечена обновленным номером версии. Наличие специальной ветки для исправления ошибок позволяет команде решать проблемы, не прерывая остальную часть рабочего процесса и не ожидая следующего цикла релиза.
Ветку hotfix можно создать с помощью следующих команд:

 * git flow hotfix start hotfix_branch

 По завершении работы ветка hotfix объединяется с master и develop:

* git flow hotfix finish hotfix_branch






