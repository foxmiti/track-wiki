# Настройка GIT этап 1

Для выполнения этой части вам необходимы минимальные знания по терминалу в ОС и минимальный набор команд для git


Git how to  - https://githowto.com/ru

Terminal - http://www.linuxrussia.com/terminal-navigation.html



# Актуальный репозиторий курса 

[tehnotrack/track18-spring](https://github.com/tehnotrack/track18-spring)


Для работы по курсу необходимо выполнить следующие действия

# Завести аккаунт на github.com
1. Завести аккаунт на github.com
2. Установить на свой рабочий компьютер git (https://git-scm.com/)
3. Прочитать немного, что это такое (например, https://githowto.com/ru)

# Сделать форк репозитория курса
Репозиторий курса доступен здесь https://github.com/tehnotrack/track18-spring
Для начала работы, вам нужно сделать fork, нажмите соответствующую кнопку в интерфейсе и вы получите копию нашего проекта в своем репозитории. (Читать на русском - http://zencoder.ru/git/fork-github/ на англ - https://help.github.com/articles/fork-a-repo/)

Теперь у вас есть собственный репозиторий с нашим проектам по адресу https://github.com/[your_name]/track18-spring, дальнейшие действия проводятся с ним.

## Склонировать репозиторий к себе на машину
Локально на компьютере создаем папку, в которой будут хранится проекты, например /Users/Dima/git
В ней зовем команду (точный адрес смотрите в своем репозитории, символ $ вводить не нужно, это просто метка, что мы вводим текст в консоли)

    $ git clone https://github.com/[your_name]/track18.git

Теперь у вас есть локальная копия проекта, с которой уже можно работать
Введите команду

    $ cd track18 (перейти в папку с проектом)
    $ git status

и удостоверьтесь, что все ок.

Проверим, что локальный репозиторий связан с удаленным на гитхабе (смотри на вывод команды). Репозиторий origin - это ваш репозиторий на гитхабе.

    $ git remote -v
    origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
    origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)

Добавим связь с общекурсовым репозиторием (upstream) и проверим:

    $ git remote add upstream https://github.com/tehnotrack/track18-spring.git
    $ git remote -v
    origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
    origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
    upstream  https://github.com/tehnotrack/track18-spring.git (fetch)
    upstream  https://github.com/tehnotrack/track18-spring.git (push)

### Синхронизация с upstream
Посколько задания выкладываются в upstream, вам нужно уметь вытягивать код оттуда. (https://help.github.com/articles/syncing-a-fork/)
Это потребуется делать при каждой новой задаче

    $ git fetch upstream (вытягиваем изменения с upstream)
    $ git checkout master (переключаемся локально на мастер)
    $ git merge upstream/master (добавляем новые изменения в свой мастер, теперь у вас самый новый код, который написал ваш преподаватель)

## Первые действия в репозитории

Создаем новый пустой файл **OWNER.md** и добавляем туда свои ФИО.
.md - это обычный текстовый файл, в котором можно использовать [markdown разметку](https://guides.github.com/features/mastering-markdown/) 

```

// Вместо vim - ваш любимый текстовый редактор, из которого вы умеете выходить
$ vim OWNER.md
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	OWNER.md

nothing added to commit but untracked files present (use "git add" to track)
```

Добавляем в index:

```
$ git add OWNER.md
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   OWNER.md
```

и комитим (сохранем состояние). С помощью ключа -m добавляем описание изменений

    $ git commit -m "Added OWNER"

Отправляем изменения на сервер (текущая ветка) идем на гитхаб и проверяем, что там появился файл с вашими данными.

    $ git push origin HEAD
    
    
После этого считаем этап 1 завершенным. Если вы все сделали правильно, то увидите изменения на github.com в своем репозитории     

