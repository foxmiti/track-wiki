# Описание
В соответствие с принципом внедрения зависимостей, при инициализации класса его компоненты должны быть внедрены снаружи через конструктор или с помощью геттеров.

Классы содержат поля, которые могут быть примитивными типами или ссылками на объекты других классов (зависимости).
Пусть есть конфигурация, описывающая все объекты, нужные в приложении и их зависимости. Тогда прочитав конфигурацию и распарсив ее, мы получим полную информацию об объектах в нашей программе.
На основании этой информации можно создавать запрашиваемые объекты. Такой инструмент называется контейнер объектов. 

20 баллов

# Формат конфига

Для проекта с классами

```java

class Car
class Engine
class Gear

```


##XML


```xml

<root>

    <bean id="carBean" class="ru.track.beans.Car">
        <property name="gear" ref="gearBean"/>
        <property name="engine" ref="engineBean"/>
    </bean>

    <bean id="gearBean" class="ru.track.beans.Gear">
        <property name="count" val="6"/>
    </bean>

    <bean id="engineBean" class="ru.track.beans.Engine">
        <property name="power" val="200"/>
    </bean>

</root>

```


* root - корневой элемент конфига
* bean - описание экземпляра класса (его полей)
  * id - уникальное имя экземпляра
  * class - определяет класс объекта

* property - описание конкретного поля
  * name - имя свойства, должно совпадать с именем поля класса
  * val - примитивное значение, или
  * ref - поле ссылается на другой объект

Этот конфиг эквивалентен такому коду:

```java
Gear gear = new Gear();
gear.setCount(6);

Engine engine = new Engine();
engine.setPower(200);

Car car = new Car();
car.setEngine(engine);
car.setPower(power);

```

## Чтение конфига
### XML

XML парсится встроенными стредствами Java https://javaswing.wordpress.com/2010/03/14/java_dom_xml/

# Задание

1) Даны классы в пакете ru.track.container: ValueType, Bean, Property. Написать класс-реализацию ConfigReader, который прочитает заданный конфиг файл, распарсит его и создаст список beans, соответствующий конфигу.

```java

public class ConfigReader {
    // чтение конфига с помощью библиотеки Jackson
    public List<Bean> readConfig(String pathToConfigFile) {
        return null;
    }
}

```

2) Инстанцирование бинов
После чтения полного конфига с помощью механизма reflection нужно инстанцировать наши объекты.

Ключевой класс - Container
```
package track.ru.track.container;

public class Container {
    private List<Bean> beans;

    /**
     * Если не получается считать конфиг, то бросьте исключение
     * @throws InvalidConfigurationException - неверный конфиг
     */
    public Container(String pathToConfig) throws InvalidConfigurationException {
    }

    /**
     *  Вернуть объект по имени бина из конфига
     *  Например, Car car = (Car) ru.track.container.getByName("carBean")
     */
    public Object getByName(String name) {
        return null;
    }

    /**
     * Вернуть объект по имени класса
     * Например, Car car = (Car) ru.track.container.getByClass("track.ru.track.container.beans.Car")
     */
    public Object getByClass(String className) {
        return null;
    }

}
```

Пример использования в коде

```java

Container ru.track.container = new Container("config.xml");
Car car = (Car) ru.track.container.getByClass("track.ru.track.container.beans.Car");

```

Договоримся, что у классов, которые создаются таким образом есть пустой конструктор, его поля - приватные, но имеют методы get/set (обратите внимание на именование метода, это важно):

```java
public class Gear {
    private int count;

    public Gear() {
    }

    public int getCount() {
        return count;
    }

    public void setCount(int count) {
        this.count = count;
    }
}

```


### ValueType

Если valueType == REF, то это означает, что поле ссылочного значения, ему нужно передать ссылку на бин с заданным именем. Если == VAL - то это значит, что поле примитивного типа.
Нужно распознать примитивный тип поля и правильно сконверить значение из конфига. Тип поля можно определить по информации из объекта Class, соответствующего бина.




