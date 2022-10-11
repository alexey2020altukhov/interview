# Собеседование Junior+
## ?. ODM
?

## ?. ООП
**Объектно-ориентированное программирование (ООП)** - это методология программирования с использованием объектов и классов. 

**Класс в Java** - это шаблон для создания объекта, а **объект** - это экземпляр класса. 
Класс определяет структуру и поведение, которые будут совместно использоваться набором объектов. Класс содержит переменные и методы, которые называются элементами класса, членами класса.

Выделяют следующие основные принципы ООП:  

**1. Абстракция** - означает выделение наиболее значимой информации и исключение из рассмотрения незначимой. С точки зрения программирования это правильное разделение программы на объекты. Абстракция позволяет отобрать главные характеристики и опустить второстепенные.  

**2. Инкапсуляция** - ограничение доступа к данным и возможностям их изменения. Инкапсуляция достигается с помощью **модификаторов доступа**:
- public - доступ из любого места программы;
- protected - доступ на уровне пакета и классов-наследников;
- default - доступ на уровне пакета;
- private - доступ только на уровне класса.

**3. Наследование** - механизм, который позволяет описать новый класс на основе уже существующего. При этом свойства и функциональность родительского класса заимствуются новым классом.  

Класс, от которого наследуются свойства и методы, называется **суперклассом (родительским классом)**. Классы, которые наследуют их, называются **подклассами (дочерними классами)**. 

Для создания дочернего класса используется ключевое слово `extends`. Для обращения к суперклассу из подкласса используется ключевое слово `super`.

_Прим:_
Множественное наследование классов в Java не допускается.

**4. Полиморфизм** - разная реализация одного и того же интерфейса.  
Полиморфизм в Java бывает статическим (полиморфизм времени компиляции) и динамическим (полиморфизм времени выполнения).  

**Перегрузка метода** является примером статического полиморфизма, а **переопределение метода** – примером динамического полиморфизма.

**Перегрузка метода** - механизм, при котором несколько методов имеют одинаковое название, но разные типы, порядок и количество параметров.
```
public int method(int a) { ... }
public int method(double a) { ... }
public int method(int a, String b) { ... }
public int method(String a, int b) { ... }
```
**Переопределение метода** - это изменение поведения в дочернем классе  уже существующего  в суперклассе метода (override).  В новом методе должны быть те же сигнатура и тип возвращаемого результата, что и у метода родительского класса.

_Прим:_
Методы с модификатором private нельзя переопределить.

## ?. Принципы SOLID
**1. Single Responsibility Principle - принцип единственной ответственности**.  
Каждый класс должен отвечать только за одну задачу. Если же существуют методы, которые не соответствуют цели сущестствования класса, их необходимо вынести за рамки этого класса.

**2. Open Closed Principle (Принцип открытости/закрытости)**.  
Классы должны быть открыты для расширений, но закрыты для модификаций. Когда вы меняете текущее поведение класса, эти изменения сказываются на всех системах, работающих с данным классом. Если хотите, чтобы класс выполнял больше операций, то идеальный вариант – не заменять старые на новые, а добавлять новые к уже существующим.

**3. Liskov’s Substitution Principle (Принцип подстановки Барбары Лисков)**.  
Подклассы должны дополнять, а не замещать поведение базового класса. Если объект базового класса заменить объектом его производного класса, то программа должна продолжить работать корректно. Необходимо, чтобы класс-потомок был способен обрабатывать те же запросы, что и родитель, и выдавать тот же результат.

**4. Interface Segregation Principle (Принцип разделения интерфейса)**.  
Лучше, когда есть множество специализированных интерфейсов, чем один общий. Не следует ставить клиент в зависимость от методов, которые он не использует. Когда классу приходится производить действия, не несущие никакой реальной пользы, это выливается в пустую трату ресурса, а в случае, если класс выполнять эти действия не способен, ведёт к возникновению багов.


**5. Dependency Inversion Principle (Принцип инверсии зависимостей)**.  
Модули верхнего уровня не должны зависеть от модулей нижнего уровня. И те, и другие должны зависеть от абстракций. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций. Этот принцип служит для того, чтобы устранить зависимость классов верхнего уровня от классов нижнего уровня за счёт введения интерфейсов.

## ?. Базовые паттерны проектирования
Паттерны проектирования — это устоявшиеся удачные решения самых распространнёх проблем, возникающих при проектировании и разработке программ или их частей.  

**1. Порождающие**  
Эти паттерны решают проблемы обеспечения гибкости создания объектов.  

**Singleton** - обеспечиват существование в системе ровно одного экземпляра некоторого класса.  
```
class Singleton {

	private Singleton instance;

	private Singleton() {}

	public static Singletot getInstance() {
		if (instance == null)
			instance = new Singleton();
		return instance;
	}
}
```
**Simple Factory** - предоставляет объект для создания других объектов, не раскрывая при этом логику.
```
public interface Door
{
    public float getWidth();

    public float getHeight();
}

public class WoodenDoor implements Door {

    private float width;
    private float height;

    public WoodenDoor(float width, float height) {
        this.width = width;
        this.height = height;
    }

    public float getWidth() {
        return this.width;
    }

    public float getHeight() {
        return this.height;
    }
}

public class DoorFactory
{
    public static Door makeDoor(float width, float height) {
        return new WoodenDoor(width, height);
    }
}

//Использование
Door door = DoorFactory.makeDoor(100, 300);
```

**Factory Method** - делегирует процесс создания объектов классам-наследникам.  

**Prototype** - клонирует объекты на основании некоторого базового объекта.  

**Builder** - отделяет процесс создания комплексного объекта от его представления.  
```
//Машина, которую хотим создать
public final class Car {
    private final String name;
    private final Color color;
    private final Brand brand;
    private final Body body;
    private final Wheels wheels;
    private final Tuning tuning;

    private Car(Builder builder) {
        this.name = builder.name;
        this.color = builder.color;
        this.brand = builder.brand;
        this.body = builder.body;
        this.wheels = builder.wheels;
        this.tuning = builder.tuning;
    }
}

//Строитель
public static class Builder {

    private final Brand brand;
    private final String name;
    private Color color;
    private Body body;
    private Wheels wheels;
    private Tuning tuning;

    /**
     * Constructor
     */
    public Builder(Brand brand, String name) {
        if (brand == null || name == null) {
            throw new IllegalArgumentException("brand and name can not be null");
        }
        this.brand = brand;
        this.name = name;
    }

    public Builder withColor(Color color) {
        this.color = color;
        return this;
    }

    public Builder withBody(Body body) {
        this.body = body;
        return this;
    }

    public Builder withWheels(Wheels wheels) {
        this.wheels = wheels;
        return this;
    }

    public Builder withTuning(Tuning tuning) {
        this.tuning = tuning;
        return this;
    }

    public Car build() {
        return new Car(this);
    }
}

//Использование
Car premiumCar = new Car.Builder(Brand.MERCEDES, "E200")
                .withBody(Body.SEDAN)
                .withColor(Color.WHITE)
                .withTuning(Tuning.WHITE)
                .withWheels(Wheels.SPORTS)
                .build();

```
**Abstract Factory** - описывает сущность для создания целых семейств взаимосвязанных объектов.  

**2. Структурные**  
Эти паттерны решают проблемы эффективного построения связей между объектами.  

**Proxy** - предоставляет объект, который контролирует доступ к другому объекту, перехватывая все вызовы (выполняет функцию контейнера).  
```
//Интерфейс
public interface WebServer {

    void makeRequest(String url);
}

//Класс, выполняющий фактическую работу
public class RealWebServer implements WebServer {
    
    @Override
    public void makeRequest(String) { ... }
}

//Прокси-класс
public class ProxyWebServer implements WebServer {

    private RealWebServer realServer;
    private List<String> blockedSites = new ArrayList<>();

    public ProxyWebServer() { 
	this.realServer = new RealWebServer(); 
    }

    public void blockWebsite(String url)  {
        this.blockedSites.add(url);
    }

    @Override
    public void makeRequest(String url) {
        if(!blockedSites.contains(url)) {
            this.realServer.makeRequest(url);
        }
        else {
 	    System.out.println("This website is blocked. Contact your administrator");
        }
    }
}
```

**Adapter** - на основании некоторого класса создает необходимый клиенту интерфейс.  

**Facade** - описывает унифицированный интерфейс для облегчения работы с набором подсистем.  

**Composite** - работает с базовыми и составными объектами единым образом.  

**Decorator** - динамически добавляет новую функциональность некоторому объекту, сохраняя его интерфейс.
```
//Интерфейс авто
public interface Car {
    public int getSpeed();
    public int getBaggageWeight();
}

//Обычный автомобиль
public class SimpleCar implements Car {
    private int speed = 50;
    private int baggageWeight = 100;

    @Override
    public int getSpeed() {
        return this.speed;
    }

    @Override
    public int getBaggageWeight() {
        return this.baggageWeight;
    }
}

//Делаем из простого автомобиля гоночный
public class SportCar implements Car {
    private Car car;
    public SportCar(Car car){
        this.car = car;
    }

    @Override
    public int getSpeed() {
        return this.car.getSpeed() + 50;
    }

    @Override
    public int getBaggageWeight() {
        return this.car.getBaggageWeight();
    }
}

//Делаем из простого автомобиля грузовой
public class Truck implements Car {
    private Car car;
    public Truck(Car car){
        this.car = car;
    }

    @Override
    public int getSpeed() {
        return this.car.getSpeed();
    }

    @Override
    public int getBaggageWeight() {
        return this.car.getBaggageWeight() + 1000;
    }
}

//Использование
Car simpleCar = new SimpleCar();
Car sportCar = new SportCar(simpleCar);
Car truck = new Truck(simpleCar);
```

**Bridge** - разделяет абстракцию от интерфейса, позволяя им меняться независимо.  

**Flyweight** - эффективно работает с огромным количеством схожих объектов.

**3. Поведенческие**  
Эти паттерны решают проблемы эффективного взаимодействия между объектами.


**Strategy** - описывает набор взаимозаменяемых алгоритмов с единым интерфейсом. 

**Iterator** - обеспечивает доступ к коллекциям объектов без раскрытия внутреннего устройства этих коллекций.  

**Observer** - создает объект для отслеживания изменений в подсистеме и нотификации других подсистем.  

**Memento** - сохраняет внутреннее состояние объекта для последующего использования без нарушения инкапсуляции.  

**Command** - описывает объект, представляющий собой некоторое действие, которое можно выполнить в необходимый момент.  

**Interpreter** - определяет способ вычисления выражений некоторого языка.  

**Mediator** - создает объект, которые регулирует взаимодействие между набором подсистем.  

**State** - позволяет объекту менять свое поведение при изменении его внутреннего состояния.  

**Template** method - описывает алгоритм, возлагая реализацию некоторых частей алгоритма на подклассы.  

**Visitor** - отделяет алгоритм от структуры, с которыми алгоритм работает.  

**Chain of responsibility** - пропускает некоторый запрос через набор обработчиков событий, до тех пор пока запрос не будет обработан.

## ?. Базовые антипаттерны
**1. God object (божественный объект)** - антипаттерн, который описывает излишнюю концентрацию слишком большого количества разношерстных функций, хранения большого количества разнообразных данных (объект, вокруг которого вращается приложение).  

**2. Magic numbers (магические числа)** - оперирование явно указанными в коде коэффициентами (как правило целочисленными), значение и смысл которых знает только автор программы.
```
this.draw(2, 320, 240, 3, 7);
```
Понятно, что это какой-то метод для рисования и больше, собственно, ничего не понятно. Чтобы это исправить нужно вводить однозначные константы или же списки Enum.

**3. Hard code** - антипаттерн, при котором код сильно привязан к конкретной аппаратной конфигурации и/или системному окружению, что сильно усложняет перенос его на другие конфигурации.
```
public Connection buildConnection() throws Exception {
   Class.forName("com.mysql.cj.jdbc.Driver");
   connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/someDb?characterEncoding=UTF-8&characterSetResults=UTF-8&serverTimezone=UTC", "user01", "12345qwert");
   return connection;
}
```
Тут мы непосредственно задаем конфигурацию нашего соединения, по итогу код будет исправно работать только с MySQL, и для смены базы данных нужно будет залезть в код и вручную всё менять.
## ?. Основные принципы проектирования
**1. YAGNI (You Aren’t Gonna Need It / Вам это не понадобится)**  
Не пишите код, который, как вам кажется, может пригодиться в будущем, но сейчас в нём потребности нет. Вскоре он станет неактуальным и его придётся переписать под конкретную задачу. 

**2. DRY (Don’t Repeat Yourself) / Не повторяйтесь**  
Все что вы пишите в проекте, должно быть определено только один раз.

**3. KISS (Keep It Simple, Stupid / Будь проще)**  
Смысл этого принципа программирования заключается в том, что стоит делать максимально простую и понятную архитектуру, применять шаблоны проектирования и не изобретать велосипед.
