# Настройка GIT этап 2

В течение курса для каждого нового задания нужно будет создать ветку для разработки

## Разработка в ветках

[что такое ветка?](https://git-scm.com/book/ru/v1/%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-Git-%D0%A7%D1%82%D0%BE-%D1%82%D0%B0%D0%BA%D0%BE%D0%B5-%D0%B2%D0%B5%D1%82%D0%BA%D0%B0%3F)
[разработка в ветках](http://habrahabr.ru/post/192614/)



## Создаем ветку
Когда на занятии дается новая задача, нужно локально создать ветку и назвать её:

[ваш_гитхаб_аккаунт]-[название_задачи], например

мой аккаунт на гитхаб = arhangeldim, задача = intro

Ветка - arhangeldim-intro

Ветки с некорректными названиями не попадают на код-ревью и не оцениваются!

Локальное создание ветки (из мастер-ветки), команда создает новую ветку и переходит в неё. Не забывайте перед этим вытянуть себе upstream(!)

    $ git fetch upstream
    $ git checkout master
    $ git merge upstream/master
    $ git checkout -b [ваш_гитхаб_аккаунт]-[название_задачи] (пусть для примера ветка называется arhangeldim-intro)


Статус нам скажет On branch arhangeldim-intro

    $ git status

Также попробуйте посмотреть команду

    $ git branch


## Отправляем задачу

Теперь вы создали ветку, **написали какой-то код** и хотите его отправить на проверку. Не торопитесь! Проверьте, что выполняются тесты и код соответсвует [style guide](https://github.com/arhangeldim/messenger/wiki/%D0%90%D0%B2%D1%82%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F-%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BA%D0%BE%D0%B4%D0%B0-(CI)#%D0%9F%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0-%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-%D0%BA%D0%BE%D0%B4%D0%B0) . (прошло некоторое время...) Ну что? поправили все? Можно дальше!

### .gitignore
Очень важный пункт, на котором фейлятся 90% студентов

Смотрим, что будет добавлено. Например, мы выполнили задание 1 и модифицировали код в App2.java

    $ git status
    
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    
    	modified:   OWNER.md
    	modified:   src/main/java/ru/track/App2.java
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
    	../.idea/
    	L1.iml
    	target/
    	
    	
Видим, что есть полезные изменения и есть некоторые служебные файлы и скомпилированный код. Эти файлы не должны попадать в ваш репозиторий.
        
        .idea/
    	L1.iml
    	target/
    	
Чтобы эти файлы никогда не попали в репозиторий, нам нужно создать специальный служебный файл .gitignore в корне проекта (уже создан в новом апдейте кода).
В этом фале нужно перечислить файлы или маски файлов, которые должны игнорироваться git. Подробнее читайте документацию git

    $ cat .gitignore
    **/*.iml
    /.idea
    **/target/
    
В разных ОС будет разный список служебных фалов, редактируйте правила с помощью .gitignore

Если в репозитории будут служебные файлы или скомпилированные классы, то такая задача не будет приниматься!



###  Комит задачи  	
    	
 Указываем, какие файлы должны попасть в репозиторий через add   	
    	
    $ git add список_файлов
    $ git commit -m "описание изменений"
    $ git push origin HEAD

  У меня примерно такой вывод после команды push:

```
   arkhangelskiy:tehnotrack-mail dmirty$ git push origin HEAD
   Counting objects: 3, done.
   Delta compression using up to 8 threads.
   Compressing objects: 100% (2/2), done.
   Writing objects: 100% (3/3), 324 bytes | 0 bytes/s, done.
   Total 3 (delta 0), reused 0 (delta 0)
   To https://github.com/arhangeldim/track16.git
      385be4a..1f66dc3  HEAD -> arhangeldim-intro
```

### код ревью (pull request)

Окей, ваш код на сервере, уже хорошо. Для проверки заданий мы используем ревью кода через pull-request.

[Хелп](https://help.github.com/articles/using-pull-requests/)

В интерфейсе github в вашем репозитории раздел branches:

![alt tag](https://raw.githubusercontent.com/arhangeldim/messenger/master/wiki/common_repo_view.png)

далее выбрать ветку с задачей и открыть pull-request:

![alt tag](https://raw.githubusercontent.com/arhangeldim/messenger/master/wiki/create_pull_req_1.png)

Теперь вы перешли в мой репозиторий и готовы создать реквест в основной репозиторий. Проверьте, что создаете реквест в ветку tehnotrack/track18-spring::master из своей ветки с задачей (В примере Okriw/messenger::Okriw-authorization)

![alt tag](https://raw.githubusercontent.com/arhangeldim/messenger/master/wiki/pull_request.png)

Когда реквест будет создан, то ваш код отправится на сборку автоматически. Сервис [непрерывной интеграции](https://ru.wikipedia.org/wiki/%D0%9D%D0%B5%D0%BF%D1%80%D0%B5%D1%80%D1%8B%D0%B2%D0%BD%D0%B0%D1%8F_%D0%B8%D0%BD%D1%82%D0%B5%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D1%8F) постарается скомпилировать ваш код, проверит форматирование и запустит тесты. Если что-то не выполнится, то билд упадет, а вы увидите ошибку с описанием. Это значит, что ваш код не работает и его надо поправить. По ссылке Details вы можете узнать подробности и посмотреть ошибки.

![alt tag](https://raw.githubusercontent.com/arhangeldim/messenger/master/wiki/ci_report.png)

Исправляйте ваш код и отправляйте изменения снова, пока не пройдут все тесты. Только после этого мы проводим код-ревью.
