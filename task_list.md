



[Презентация на GitHub](https://raw.githubusercontent.com/darkwrat/track17-autumn/stuff/L3.pdf)
[Скринкаст занятия на GitHub](https://raw.githubusercontent.com/darkwrat/track17-autumn/stuff/xxx.mp4)

##Задача "list"

1) Обновите свой репозиторий с апстрима по инструкции
2) Создайте новую ветку в соответствии с инструкцией [ваш_гитхаб_аккаунт]-[название_задачи], где название задачи - list
3) Если вы дописывали @Ignore на методы тестирования - уберите.
4) Напишите код, часть инструкций есть в коде
5) Убедитесь, что тесты  прошли 


Дописать классы из пакета ru.track.list модуля L3 (L3-oop): List, MyArrayList, MyLinkedList (не используйте классы стандартной библиотеки!).
Классы будут работать с int, то есть это списки целых чисел.
Каждый класс должен лежать в своем файле.

Класс List - родительский, абстрактный, его экземпляр создать нельзя.

MyArrayList - список на основе массива, массив должен динамически расширяться, если в старом не хватает места для элемента. Для
копирования массива следует использовать метод [System.arraycopy()](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#arraycopy-java.lang.Object-int-java.lang.Object-int-int-)

MyLinkedList - список на основе, (что бы вы думали?) связного списка, каждый узел списка содержит ссылку на предыдущий и следующий узел.

```
class Node {
    private Node next;
    private Node prev;
    privtae int value;
    // конструктор, методы и т п
```

У класса List должны быть объявлены (не обязательно определены, возможно abstract) методы:
Внимание! не меняйте сигнатуры!

```
class List {
    void add(int item); - добавить элемент в конец списка
    int remove(int idx); - удалить элемент по индексу idx, если idx некорректный напечатать ошибку, если ок - вернуть удаленный элемент
    int get(int idx); - получить элемент по индексу
    int size(); - сколько элементов в данный момент в списке
 }
```

Также, класс LinkedList (тот что на основе связного списка) должен реализовывать интерфейс Stack и Queue и определить реализацию соответствующих методов.

Интерфейсы определить в отдельных файлах в той же директории

```
// Стек - структура данных, удовлетворяющая правилу Last IN First OUT
interface Stack {
    void push(int value); // положить значение наверх стека
    int pop(); // вытащить верхнее значение со стека
}

// Очередь - структура данных, удовлетворяющая правилу First IN First OUT
interface Queue {
    void enqueue(int value); // поместить элемент в очередь
    int dequeu(); // вытащить первый элемент из очереди
}

```




Еще раз скажу, нельзя использовать стандартные классы коллекций из Java
Обратите внимание на использование модификаторов доступа, не должно остаться полей и методов без модификаторов.

## Бонус

Кто напишет тесты на свой код, получит бонусные баллы!

##Книги по курсу: 

Названия тем в кингах примерно совпадает с нашими, в данном случае нужно читать про объекты, наследование, полиморфизм, интерфейсы

(Objects, inheritance, polymorphism, interface)

Брюс Эккель - Философия Java
Кей С. Хорстманн, Гари Корнелл, "Java. Библиотека профессионала, том 1. Основы"


##Хороший сайт с материалами по Java - skipy.ru (давно не появляются новые статьи, но это кладезь знаний, отличный фундамент)

Наследование http://skipy.ru/philosophy/inheritance.html
Принципы дизайна приложений http://skipy.ru/architecture/module_design.html

##Еще немного ссылок

http://blog.byndyu.ru/2009/12/blog-post.html

Документация Java http://docs.oracle.com/javase/8/docs/api/

Туториалы Java https://docs.oracle.com/javase/tutorial/


Про модификаторы (final в том числе) http://www.javenue.info/post/java-modifiers-summary

Почему появились default-методы в интерфейсах https://blog.idrsolutions.com/2015/01/java-8-default-methods-explained-5-minutes/

#Домашнее задание
Самостоятельно разобраться с ключевыми словами super/this и их использованием в конструкторе
http://developer.alexanderklimov.ru/android/java/extends.php

Разобраться с перечисляемымми типами (enum)
http://developer.alexanderklimov.ru/android/java/enum.php

паттерн проектирования Команда
http://articles.javatalks.ru/articles/3






     
