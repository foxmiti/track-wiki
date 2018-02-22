## Database

Срок сдачи до 20.12

Оценка 20 баллов


В рамках задачи про потоки - Клиент-Серверный чат нужно реализовать сохранение сообщений в базу.

Примечание - если у вас нет сервера, то попробуйте реализовать только часть связанную с работой с БД

Работать можно в ветке threads, где вы делали сервер. Нам потребуется сохранять в базу текстовые сообщения вида:

```java

class Message {
  String senderName;
  String text;
  long timestamp;
}

```

### Шардирование

Для задачи заведена общая база. Особенность в том, что база шардирована на 3 хоста, то есть данные распределены.

Вот адреса машин:
* tdb-1.trail5.net
* tdb-2.trail5.net
* tdb-3.trail5.net

У нас данные шардированы по имени отправителя по следущему правилу. Нужно смотреть на первый символ имени пользователя и определить по нему на какой шард идти

* A-J -> tdb-1.trail5.net
* K-T > tdb-2.trail5.net
* U-Z -> tdb-3.trail5.net

(регистр значения не имеет, имена начинающиеся не с буквы не допускаются)


###Подключение к базе
```
для шарда 1 соответственно

jdbc:mysql://tdb-1.trail5.net:3306/track17 


user=track_student
password=7EsH.H6x

```


В базе заведена таблица для сообщений. Есть поле ID которое работает как атомарный счетчик и увеличивается на 1 при каждой вставке. 
Его не нужно добавлять вручную.

```sql
CREATE TABLE `messages` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `user_name` varchar(256) DEFAULT NULL,
  `text` text,
  `ts` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=33 DEFAULT CHARSET=latin1


```


###  АПИ к хранилищу

```java
public interface ConversationService {
    /**
     * В зависимости от Message.senderName нужно сохранять в разные базы
     * 
     * @return вернуть ID, который был присвоен сообщению в базе (поле ID)
     * 
     * 
     * 4 балла
     */
    long store(Message msg);
    
    /**
    * Получить историю сообщений за период времени. Важно учесть лимит, чтобы не свалить базы слишком большой выборкой.
    *      Ограничить LIMIT нужно именно при запросе в базу
    * @param from - timestamp с какого времени
    * @param to - timestamp до какого времени
    * @param limit - максимальное кол-во ссобщений
    * 
    * @return Список, отсротированный по timestamp
    * 
    * 4 балла
    */
    List<Message> getHistory(long from, long to, long limit);
    
 
    /**
    * Вернуть все сообщения от определенного пользователя 
    * 
    * 4 балла
    */
    List<Message> getByUser(String username, long limit);
    
}

```

### Примечания

1) для того, чтобы store(Message msg) вернул id вам потребуется посмотреть на 
    https://docs.oracle.com/javase/8/docs/api/java/sql/Connection.html#prepareStatement-java.lang.String-int-
    https://docs.oracle.com/cd/E17952_01/connector-j-en/connector-j-usagenotes-last-insert-id.html
    https://stackoverflow.com/questions/1915166/how-to-get-the-insert-id-in-jdbc

2) getHistory - должен смерджить списки сообщений со всех шардов. Подумайте, как ваш код будет работать при недоступности одного из шардов

3) Желательно научить ваш сервер отправлять ответы из базы на клиент и распечатывать их там в читаемом виде

4) Для работы с базой использовать PreparedStatement (не просто Statement)


12 баллов за реализацию методов
+4 балла за встроенность в сервер и отдачу на клиенты
+4 за хорошую архитектуру и обработку ошибок





