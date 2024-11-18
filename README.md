### Собеседование Junior+
## Оглавление

[Типы данных](#data-types)  
[ООП](#oop)  
[Принципы SOLID](#solid)  
[Базовые паттерны проектирования](#basic-design-patterns)  
[Паттерны MCA](#mca-patterns)  
[Базовые антипаттерны](#basic-antipatterns)  
[Основные принципы проектирования](#basic-design-principles)  
[Ассоциация: агрегация и композиция](#association)  
[Git](#git)  
[Spring](#spring)  
[Аннотации @Controller и @RestController](#controller-restcontroller)  
[@Component, @Repository, @Service, @Controller](#component-repository-service-controller)  
[Другие аннотации Spring](#other-spring-annotations)  
[Транзации Spring](#spring-transactions)  
[Spring контейнеры](#spring-containers)  
[BeanFactoryPostProcessor и BeanPostProcessor](#bean-post-processor)  
[JVM, JDK, JRE](#jvm-jdk-jre)  
[Аннотации](#annotations)  
[Абстрактный класс VS интерфейс](#abstract-class-vs-interface)  
[Ключевые слова static и final](#static_and_final)  
[ACID](#acid)  
[Коллекции](#collections)  
[Сборщик мусора (Garbage Collector)](#garbage-collector)  
[SOAP](#soap)  
[REST](#rest)  
[Асинхронное/синхронное общение](#async-sync-communication)  
[Kafka](#kafka)  
[Exceptions (Исключения)](#exceptions)  
[Алгоритмическая сложность(O-нотация)](#o-notation)  
[Иммутабельность в Java](#immutability)  
[Heap и Stack память](#heap-stack)  
[Класс Object и его методы](#object-class-and-methods)  
[Потоки IO](#io-streams)  
[Вложенные и внутренние классы](#nested-internal-classes)  
[Структуры данных](#data-structures)  
[Stream Api Java](#stream-api)  
[БД](#db)  
[Сборщики/maven](#assemblers)  
[CI/CD](#ci-cd)  
[Kotlin](#kotlin)  
[Ошибка N+1](#error-n+1)  
[Сериализация и десериализация](#serialization-deserialization)  
[Многопоточность Java](#multithreading)  
[Лямбда-выражения](#lambda-expressions)  
[Решение заданий](#task-solutions)

## Дописать вопросы по темам
- ODM
- Классы-обёртки
- Брокеры сообщений
- KeyCloak

<a name="data-types"/>  

## Типы данных

В Java типы данных делят на две большие группы: примитивные и ссылочные.
![image](https://user-images.githubusercontent.com/73114969/217656237-4d56634a-e3a9-4740-9361-67bd69c60fc6.png)

Ссылочные типы данных ещё называют ссылками. К ним относятся все классы, интерфейсы, массивы, а также тип данных String. В отличие от примитивов, которые хранят значения, ссылочные типы хранят адрес объекта в памяти, на который ссылаются.

<a name="oop"/>  

## ООП
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

<a name="solid"/>  

## Принципы SOLID
**1. Single Responsibility Principle - принцип единственной ответственности**.  
Каждый класс должен отвечать только за одну задачу (должна быть лишь одна причина для его изменения). Если же существуют методы, которые не соответствуют цели сущестствования класса, их необходимо вынести за рамки этого класса. 

**2. Open Closed Principle (Принцип открытости/закрытости)**.  
Классы должны быть открыты для расширений, но закрыты для модификаций. Когда вы меняете текущее поведение класса, эти изменения сказываются на всех системах, работающих с данным классом. Если хотите, чтобы класс выполнял больше операций, то идеальный вариант – не заменять старые на новые, а добавлять новые к уже существующим.

**3. Liskov’s Substitution Principle (Принцип подстановки Барбары Лисков)**.  
Подклассы должны дополнять, а не замещать поведение базового класса. Если объект базового класса заменить объектом его производного класса, то программа должна продолжить работать корректно. Необходимо, чтобы класс-потомок был способен обрабатывать те же запросы, что и родитель, и выдавать тот же результат.

**4. Interface Segregation Principle (Принцип разделения интерфейса)**.  
Лучше, когда есть множество специализированных интерфейсов, чем один общий. Не следует ставить клиент в зависимость от методов, которые он не использует. Когда классу приходится производить действия, не несущие никакой реальной пользы, это выливается в пустую трату ресурса, а в случае, если класс выполнять эти действия не способен, ведёт к возникновению багов.

**5. Dependency Inversion Principle (Принцип инверсии зависимостей)**.  
Модули верхнего уровня не должны зависеть от модулей нижнего уровня. И те, и другие должны зависеть от абстракций. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций. Этот принцип служит для того, чтобы устранить зависимость классов верхнего уровня от классов нижнего уровня за счёт введения интерфейсов.

<a name="basic-design-patterns"/>  

## Базовые паттерны проектирования
Паттерны проектирования — это устоявшиеся удачные решения самых распространнёх проблем, возникающих при проектировании и разработке программ или их частей.  

**1. Порождающие**  
Эти паттерны решают проблемы обеспечения гибкости создания объектов.  

**Singleton** - обеспечиват существование в системе ровно одного экземпляра некоторого класса.  
<details>
  <summary>Пример</summary>
	
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
</details>

**Simple Factory** - предоставляет объект для создания других объектов, не раскрывая при этом логику.
<details>
  <summary>Пример</summary>
	
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
</details>

**Builder** -  позволяет поэтапно создавать сложные объекты.  
<details>
  <summary>Пример</summary>
	
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
</details>

**Prototype** - создает новые объекты, копируя существующие.  

**Factory Method** - делегирует процесс создания объектов классам-наследникам.  

**Abstract Factory** - описывает сущность для создания целых семейств взаимосвязанных объектов.  

**2. Структурные**  
Эти паттерны решают проблемы эффективного построения связей между объектами.  

**Proxy** - предоставляет объект, который контролирует доступ к другому объекту, перехватывая все вызовы (выполняет функцию контейнера).  
<details>
  <summary>Пример</summary>
	
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
</details>

**Decorator** - динамически добавляет новую функциональность некоторому объекту, сохраняя его интерфейс.
<details>
  <summary>Пример</summary>
	
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
</details>

**Adapter** - на основании некоторого класса создает необходимый клиенту интерфейс.  

**Facade** - описывает унифицированный интерфейс для облегчения работы с набором подсистем.  

**Composite** - работает с базовыми и составными объектами единым образом.  

**Bridge** - разделяет абстракцию от интерфейса, позволяя им меняться независимо.  

**Flyweight** - эффективно работает с огромным количеством схожих объектов.

**3. Поведенческие**  
Эти паттерны решают проблемы эффективного взаимодействия между объектами.

**Strategy** - описывает набор взаимозаменяемых алгоритмов с единым интерфейсом. 
<details>
  <summary>Пример</summary>
	
  ```
public class Computer {
    private ComputerStrategy strategy;

    public Computer(ComputerStrategy strategy){
        this.strategy = strategy;
    }

    public void setNewTask(ComputerStrategy strategy){
        this.strategy = strategy;
    }

    public void runTask() {
        this.strategy.execute();
    }
}

// Computer может выполнять много разных алгоритмов-заданий
// Они приходят к нему через контруктор либо через метод setNewTask. Вот примеры алгоритмов-заданий:

public class Video implements ComputerStrategy {
    private static final Logger LOGGER = Logger.getLogger(Video.class.getName());

    @Override
    public void execute() {
        LOGGER.info("Video playing");
    }
}

public class Music implements ComputerStrategy {
    private static final Logger LOGGER = Logger.getLogger(Music.class.getName());

    @Override
    public void execute() {
        LOGGER.info("Music playing");
    }
}

// Каждый из этих алгоритмов реализует интерфейс ComputerStrategy:

@FunctionalInterface
public interface ComputerStrategy {
    void execute();
}

public class App {
    private static final Logger LOGGER = Logger.getLogger(App.class.getName());

    public static void main(String[] args){
        LOGGER.info("Switch on computer and play movie");
        Computer computer = new Computer(new Video());
        computer.runTask();

        LOGGER.info("Find music");
        computer.setNewTask(new Music());
        computer.runTask();

        // Java 8
        Computer functionalComputer = new Computer(
                () -> LOGGER.info("Write program")
        );
        functionalComputer.runTask();

        functionalComputer = new Computer(
                () -> LOGGER.info("Execute some code and get some output")
        );
        functionalComputer.runTask();
    }
}
```
</details>

**Iterator** - обеспечивает доступ к коллекциям объектов без раскрытия внутреннего устройства этих коллекций.  

**Chain of Responsibility** - позволяет передавать запросы последовательно по цепочке обработчиков. Каждый последующий обработчик решает, может ли он обработать запрос сам и стоит ли передавать запрос дальше по цепи.
<details>
  <summary>Пример</summary>
	
  ```
public abstract class AuthenticationProcessor {

    public AuthenticationProcessor nextProcessor;

    public abstract boolean isAuthorize (AuthenticationProvider authProvider);
}

public class OAuthProcessor extends AuthenticationProcessor {

    public OAuthProcessor(AuthenticationProcessor nextProcessor) {
        super(nextProcessor);
    }

    @Override
    public boolean isAuthorized(AuthenticationProvider authProvider) {
        if (authProvider instanceof OAuthTokenProvider) {
            return true;
        } else if (nextProcessor != null) {
            return nextProcessor.isAuthorized(authProvider);
        }
        
        return false;
    }
}

public class UsernamePasswordProcessor extends AuthenticationProcessor {

    public UsernamePasswordProcessor(AuthenticationProcessor nextProcessor) {
        super(nextProcessor);
    }

    @Override
    public boolean isAuthorized(AuthenticationProvider authProvider) {
        if (authProvider instanceof UsernamePasswordProvider) {
            return true;
        } else if (nextProcessor != null) {
            return nextProcessor.isAuthorized(authProvider);
        }
    return false;
    }
}

public class ChainOfResponsibilityTest {

    private static AuthenticationProcessor getChainOfAuthProcessor() {
        AuthenticationProcessor oAuthProcessor = new OAuthProcessor(null);
        return new UsernamePasswordProcessor(oAuthProcessor);
    }

    @Test
    public void givenOAuthProvider_whenCheckingAuthorized_thenSuccess() {
        AuthenticationProcessor authProcessorChain = getChainOfAuthProcessor();
        assertTrue(authProcessorChain.isAuthorized(new OAuthTokenProvider()));
    }

    @Test
    public void givenSamlProvider_whenCheckingAuthorized_thenSuccess() {
        AuthenticationProcessor authProcessorChain = getChainOfAuthProcessor();
 
        assertFalse(authProcessorChain.isAuthorized(new SamlTokenProvider()));
    }
}
```
</details>

**Observer** - создает объект для отслеживания изменений в подсистеме и нотификации других подсистем.  

**Memento** - сохраняет внутреннее состояние объекта для последующего использования без нарушения инкапсуляции.  

**Command** - описывает объект, представляющий собой некоторое действие, которое можно выполнить в необходимый момент.  

**Interpreter** - определяет способ вычисления выражений некоторого языка.  

**Mediator** - создает объект, которые регулирует взаимодействие между набором подсистем.  

**State** - позволяет объекту менять свое поведение при изменении его внутреннего состояния.  

**Template** method - описывает алгоритм, возлагая реализацию некоторых частей алгоритма на подклассы.  

**Visitor** - отделяет алгоритм от структуры, с которыми алгоритм работает.  

<a name="mca-patterns"/>  

## Паттерны MCA
**Saga** - предоставляет механизм, который позволяет обеспечить согласованность данных в микросервисной архитектуре без применения распределенных транзакций.

Сага представляет собой набор локальных транзакций. Каждая локальная транзакция обновляет базу данных и публикует сообщение или событие, инициируя следующую локальную транзакцию в саге. Если транзакция завершилась неудачей, например, из-за нарушения бизнес правил, тогда сага запускает компенсирующие транзакции, которые откатывают изменения, сделанные предшествующими локальными транзакциями.

Типы транзакций в саге:

- Компенсирующая — отменяет изменение, сделанное локальной транзакцией.
- Компенсируемая — это транзакция, которую необходимо компенсировать (отменить) в случае, если последующие транзакции завершаются неудачей.
- Поворотная — транзакция, опеределяющая успешность всей саги. Если она выполняется успешно, то сага гарантированно дойдет до конца.
- Повторяемая — идет после поворотной и гарантированно завершается успехом.

Существует два способа координации саг:  
- Хореография (Choreography) — каждая транзакция публикует события, которые запускают транзакции в других сервисах.
- Оркестровка (Orchestration) — оркестратор говорит участникам, какие транзакции должны быть запущены.

**Transactional Outbox** описывает общий подход для хранения завершенных транзакций. При выполнении транзакции (например, когда идёт сохранение какой-либо сущности) в рамках этой же транзакции также сохраняется информация об этом действии в отдельную таблицу (например, outbox). Потом сторонний scheduler через определенные интервалы времени заглядывает в эту таблицу. Если запись там есть, то выполняет следующую транзакцию (или отправляет данные в брокер сообщений).

Если бизнес-объект и соответствующие сообщения сохраняются в рамках одной транзакции базы данных, это гарантирует, что данные не будут потеряны. Либо будет зафиксировано все, либо при возникновении ошибки произойдет полный откат.

**Circuit Breaker** предотвращает попытки приложения выполнить операцию, которая скорее всего завершится неудачно, что позволяет продолжить работу дальше не тратя важные ресурсы, пока известно, что проблема не устранена. Приложение должно быстро принять сбой операции и обработать его.

Он также позволяет приложению определять, была ли устранена неисправность. Если проблема устранена, приложение может попытаться вызвать операцию снова.

Например, один микросервис отправляет запрос к другому микросервису. Паттерн позволяет не ждать ответа, а сразу вернуть ошибку в случае его недоступности.

<a name="basic-antipatterns"/>  

## Базовые антипаттерны
**1. God object (божественный объект)** - антипаттерн, который описывает излишнюю концентрацию слишком большого количества разношерстных функций, хранения большого количества разнообразных данных (объект, вокруг которого вращается приложение).  

**2. Magic numbers (магические числа)** - оперирование явно указанными в коде коэффициентами (как правило целочисленными), значение и смысл которых знает только автор программы.
<details>
  <summary>Пример</summary>
	
  ```
this.draw(2, 320, 240, 3, 7);
```
Понятно, что это какой-то метод для рисования и больше, собственно, ничего не понятно. Чтобы это исправить нужно вводить однозначные константы или же списки Enum.
</details>

**3. Hard code** - антипаттерн, при котором код сильно привязан к конкретной аппаратной конфигурации и/или системному окружению, что сильно усложняет перенос его на другие конфигурации.
<details>
  <summary>Пример</summary>
	
  ```
public Connection buildConnection() throws Exception {
   Class.forName("com.mysql.cj.jdbc.Driver");
   connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/someDb?characterEncoding=UTF-8&characterSetResults=UTF-8&serverTimezone=UTC", "user01", "12345qwert");
   return connection;
}
```
Тут мы непосредственно задаем конфигурацию нашего соединения, по итогу код будет исправно работать только с MySQL, и для смены базы данных нужно будет залезть в код и вручную всё менять.
</details>

<a name="basic-design-principles"/>  

## Основные принципы проектирования
**1. YAGNI (You Aren’t Gonna Need It / Вам это не понадобится)**  
Не пишите код, который, как вам кажется, может пригодиться в будущем, но сейчас в нём потребности нет. Вскоре он станет неактуальным и его придётся переписать под конкретную задачу. 

**2. DRY (Don’t Repeat Yourself) / Не повторяйтесь**  
Этот принцип заключается в том, что нужно избегать повторений одного и того же кода.

**3. KISS (Keep It Simple, Stupid / Будь проще)**  
Смысл этого принципа программирования заключается в том, что стоит делать максимально простую и понятную архитектуру, применять шаблоны проектирования и не изобретать велосипед.

<a name="association"/>  

## Ассоциация: агрегация и композиция

Классы и объекты могут быть связаны друг с другом. Наследование описывает связь «является». Лев является животным. Такое отношение легко выразить с помощью наследования, где Animal будет родительским классом, а Lion — потомком.
Однако не все связи отношения в мире описываются таким образом. К примеру, клавиатура определенно как-то связана с компьютером, но она не является компьютером. Руки как-то связаны с человеком, но они не являются человеком. В этих случаях в его основе лежит другой тип отношения: не «является», а «является частью».  

**Ассоциация** означает, что объекты двух классов могут ссылаться один на другой, иметь некоторую связь между друг другом. Ассоциация описывается словом «имеет». Агрегация и композиция на самом деле являются частными случаями ассоциации.

**Агрегация** - вид ассоциации, который указывает, что один класс является частью другого. Например, студент входит в группу по рисованию. Агрегация образует слабую связь между объектами. Все зависимые классы инициализируются вне основного объекта, и передаются, например, в конструкторе этого класса.  

**Композиция** - определяет более «жесткое отношение», при котором один объект может быть только частью другого объекта. Например машина и двигатель. Хотя двигатель может быть и без машины, но он вряд ли сможет быть в двух или трех машинах одновременно.

<a name="git"/>  

## Git
**Git** - это распределенная система контроля версий.

**Другие системы контроля версий (VCS)**
- Mercurial
- Subversion

**Основные понятия**
- Репозиторий - это каталог файловой системы, в котором в Git отслеживаются изменения.
- Удалённый репозиторий - репозиторий, находящийся на удалённом сервере.
- Локальный репозиторий - репозиторий, расположенный на локальном компьютере разработчика в каталоге (копия удаленного репозитория).
- Форк (Fork) - копия репозитория. Его также можно рассматривать как внешнюю ветку для текущего репозитория.
- Клонирование (Clone) — скачивание репозитория с удалённого сервера на локальный компьютер в определённый каталог для дальнейшей работы с этим каталогом как с репозиторием.
- Мастер (Master) - главная или основная ветка репозитория.
- Коммит - фиксация изменений или запись изменений в репозиторий. Коммит происходит на локальной машине.
- Ветка - это подвижный указатель на один из коммитов.
- Merge - объединение (слияние) двух или более веток. В процессе мерджа изменения с указанной ветки переносятся (копируются) в текущую.
- Rebase - еще один способ перенести изменения из одной ветки в другую. Rebase сжимает все изменения в один «патч». Затем он интегрирует патч в целевую ветку.
- Merge коммит - коммит, который создается автоматически по завершению процесса слияния веток. Мердж коммит содержит в себе все изменения целевой ветки мерджа, которые отсутствуют в текущей (все коммиты целевой ветки, которые начиная с базы слияния, но не включая её).
- Merge конфликт - ситуация, когда при слиянии веток в один или несколько файлов вносились независимые изменения. В некоторых случаях (например, если изменялись разные, не пересекающиеся части одного файла) git способен самостоятельно решить, как выполнять слияние таких файлов. Если автоматически это сделать не удалось — возникает конфликт. В таком случае необходимо самостоятельно указать, как выполнять слияние конфликтующих версий (решить конфликт, resolve merge conflict).
- Дифф (diff) - разница двух состояний (коммитов, веток, подготовленных или модифицированных файлов).
- Черри-пик (cherry-pick) - процесс добавления в текущую ветку одного (или нескольких) коммитов из другой ветки, без необходимости выполнять слияние веток.
- Пуш (Push) - отправка всех неотправленных коммитов на удалённый сервер репозитория.
- Пул (Pull) - получение последних изменений с удалённого сервера репозитория.
- Пулреквест (Pull Request) - запрос на слияние форка репозитория с основным репозиторием. Пулреквест может быть принят или отклонён вами, как владельцем репозитория.

**Некоторые команды Git**  

Инициализация репозитория:
```
git init
```
Добавление отдельных файлов в область подготовленных файлов:
```
git add test.txt
```
Добавление всех файлов в область подготовленных файлов:
```
git add .
```
Проверка статуса репозитория:
```
git status
```
Коммит:
```
git commit -m "Init commit"
```
Отмена изменений. Данная команда создаёт еще один коммит, который выполняет изменения, противоположные тому коммиту, который отменяется:
```
git revert aa600a43cb164408e4ad87d216bc679d097f1a6c
```
Удаление последнего коммита. В отличие от revert не создаёт коммита и является небезопасной командой. Флаг --hard означает полное удаление:
```
git reset --hard HEAD~
```
Создание новой ветки:
```
git branch branch_name
```
Создание новой ветки и переключение на неё:
```
git checkout -b branch_name
```
Посмотреть полный список веток:
```
git branch
```
Удаление локальной ветки:
```
git branch -D branch_name
```
Слияние двух веток:
```
git merge branch_name
```
Отправка изменений в удаленный репозиторий:
```
git push origin main
```
Получение изменений из удаленного репозитория и слияние изменений с рабочей веткой (git fetch + git merge):
```
git pull
```
Получение изменений из удаленного репозитория без слияния изменений. Чтобы их слить в рабочую ветку необходимо сделать merge:
```
git fetch
```

<a name="spring"/>  

## Spring
По сути **Spring Framework** представляет собой просто контейнер внедрения зависимостей, с несколькими удобными слоями (доступ к базе данных, прокси, аспектно-ориентированное программирование, RPC, веб-инфраструктура MVC). Это все позволяет быстрее и удобнее создавать Java-приложения.

Ключевая особенность приложения, написанного на Spring, состоит в том что большую часть объектов создаем не мы, а Spring. Мы лишь конфигурируем классы (с помощью аннотаций либо в конфигурационном XML), чтобы «объяснить» фреймворку Spring, какие именно объекты он должен создать за нас, и полями каких объектов их сделать. Это и называется **инверсией управления** или **IoC (Inversion of Control)**. Объекты, которые создаются контейнером и находятся под его управлением, называются **бинами.** Внедрение зависимости **(Dependency Injection)** — это и есть инициализация полей бинов другими бинами (зависимостями).

**Области видимости (scope) бинов:**
- Singleton (по умолчанию). Бин с данным именем создаётся 1 раз в Spring Application Context и каждый раз при вызове getBean() вызывается тот самый бин. Используется, когда у бина нет изменяемых состояний (stateless)
- Prototype. При вызове getBean() каждый раз будет создаваться новый бин в Spring Application Context. Используется, когда у бина есть изменяемые состояния (statefull)
- Request. Создаётся один экземпляр бина на каждый HTTP запрос. Касается исключительно ApplicationContext.
- Session. Создаётся один экземпляр бина на каждую HTTP сессию. Касается исключительно ApplicationContext.
- Global-session. Создаётся один экземпляр бина на каждую глобальную HTTP сессию. Используется только с портлетами. Касается исключительно ApplicationContext.

**Способы внедрения бинов:**
- Через конструктор. Преимущество: отсутствие рефлексии, внедрение зависимостей будет работать даже при использовании другого контейнера (не Spring). 
<details>
  <summary>Пример</summary>

```
private DependencyA dependencyA;
private DependencyB dependencyB;
private DependencyC dependencyC;

@Autowired
public DI(DependencyA dependencyA, DependencyB dependencyB, DependencyC dependencyC) {
    this.dependencyA = dependencyA;
    this.dependencyB = dependencyB;
    this.dependencyC = dependencyC;
}
```
А можно просто воспользоваться аннотацией ``@RequiredArgsContructor``, повесив её над классом, и пометить необходимые поля как final.
</details>

- Через поле. Недостаток: Spring через рефлексию подтягивает это поле (у класса найдёт это поле и по нему найдет зависимость которую надо внедрить). Следовательно - более слабый перформанс. Преимуществом является то, что IDEA сразу подсвечивает нам какой бин внедрён (если бин не внедрён, IDEA об этом скажет).
<details>
  <summary>Пример</summary>

```@Autowired
private DependencyA dependencyA;
@Autowired
private DependencyB dependencyB;
@Autowired
private DependencyC dependencyC;

```
</details>

- Через сеттер (устарело)
<details>
  <summary>Пример</summary>

```
private DependencyA dependencyA;
private DependencyB dependencyB;
private DependencyC dependencyC;

@Autowired
public void setDependencyA(DependencyA dependencyA) {
    this.dependencyA = dependencyA;
}

@Autowired
public void setDependencyB(DependencyB dependencyB) {
    this.dependencyB = dependencyB;
}

@Autowired
public void setDependencyC(DependencyC dependencyC) {
    this.dependencyC = dependencyC;
}
```
</details>

**Способы создать Bean:**  
- Через XML.
<details>
  <summary>Пример</summary>

```
<beans>
   <!-- A simple bean definition -->
   <bean id = "fromBeanMessage" class = "com.example.Message">
       <property name="message" value="This is message from simple bean"/>
      <!-- collaborators and configuration for this bean go here -->
   </bean>
   <!-- A bean definition with lazy init set on -->
   <bean id = "lazy" class = "com.example.Lazy" lazy-init = "true">
      <!-- collaborators and configuration for this bean go here -->
   </bean>
   <!-- A bean definition with initialization method -->
   <bean id = "init" class = "com.example.Message" init-method = "getMessage">
      <!-- collaborators and configuration for this bean go here -->
   </bean>
   <!-- A bean definition with destruction method -->
   <bean id = "destroyBean" class = "com.example.Message" destroy-method = "getMessage">
      <!-- collaborators and configuration for this bean go here -->
   </bean>
</beans>
```
</details>

- Через аннотацию ``@Component`` - вешается над классом, говоря спрингу, что от данного класса нужно создать бин.
- Через аннотацию ``@Bean`` - вешается над методом, возвращаемое значение которого будет являться бином. Используется в классах помеченных ``@Configuration``.

Аннотация ``@Bean`` чаще всего используется в тех случаях, когда необходимо создать бин из класса, который изначально не предназначался для внедрения в Spring Application Context (например, класс из сторонних библиотек). Аннотация ``@Component`` указывается обычно над каким-нибудь пользовательским классом.

<a name="controller-restcontroller"/>  

## Аннотации @Controller и @RestController

``@Controller`` - это специализация универсальной стереотипной @Component, которая указывает Spring, что класс выполняет функцию контроллера и принимает входящие HTTP-запросы.

@Controller расширяет возможности использования @Component и отмечает аннотированный класс как бизнес-уровень или уровень представления. Когда запрос сделан, это проинформирует DispatcherServlet о включении класса контроллера в сканирование методов, отображаемых аннотацией ``@RequestMapping``.

``@RestController`` в Spring по сути представляют собой просто комбинацию ``@Controller`` и ``@ResponseBody``.

``@ResponseBody`` позволяет сериализовать возвращаемый объект в
JSON или XML и отправить эту информацию обратно как часть HTTP-ответа.

``@RequestBody`` сопоставляет тело HttpRequest с объектом transfer или domain и проводит автоматическую десериализацию входящего тела HttpRequest в объект Java.

Сначала запрос получает DispatcherServlet , который отвечает за обработку любых входящих запросов URI и сопоставление их с соответствующими обработчиками в виде методов контроллера. После выполнения метода контроллера ресурс обрабатывается как ответ, который может быть либо JSON, либо XML.

Аннотация ``@RequestMapping`` используется для мапинга (связывания) с URL для всего класса или для конкретного метода обработчика.

DispatcherServlet будет искать ``@RequestMapping`` для классов, которые аннотируются с помощью ``@Controller``.

<a name="component-repository-service-controller"/>  

## @Component, @Repository, @Service, @Controller

Все эти аннотацию имеют общую семантику.

1. Аннотация @Component применяется при указании класса в качестве Spring-компонента. В результате, в случае использования поиска аннотаций обозначенный таким образом класс сконфигурируется как Spring Bean. 
2. Аннотация -- @Controller -- представляет собой специальный тип класса, который используется в MVC-приложениях. Служит для обработки запросов и нередко применяется совместно с аннотацией @RequestMapping.
3. Аннотация @Repository показывает, что класс применяется для работы с поиском, а также для получения и хранения данных. На практике @Repository может применяться при реализации шаблона DAO.
4. Аннотация @Service показывает, что класс представляет собой сервис для реализации бизнес-логики. По сути, аннотация не отличается от Component, однако она помогает программисту указать смысловую нагрузку используемого класса.

<a name="other-spring-annotations"/>  

## Другие аннотации Spring

1. ``@ComponentScan`` вместе с аннотацией ``@Configuration`` позволяет указать пакеты, которые мы хотим сканировать. ``@ComponentScan`` без аргументов указывает Spring сканировать текущий пакет и все его подпакеты.
2. ``@Autowired`` используется для автоматического внедрения зависимостей в компоненты приложения. В SpringApplicationContext хранятся все бины (Классы, на которых висит ``@Component`` или их бин создан в явном виде в xml или через @Bean). ``@Autowired`` внедряет ссылку на существующий бин в поле, над которым висит ``@Autowired``. Если scope бина “prototype”, то при ``@Autowired`` полю присваивается ссылка на новый бин. 

Прим.: Внедрять зависимости через ``@Autowired`` следует через конструктор, т.к через конструктор зависимости могут быть final, а значит потокобезопасными. Также, можно не писать @InjectMocks при написании юнит-тестов.

3. ``@Qualifier``. Используется для указания конкретного бина для внедрения в другой бин при условии, что есть несколько бинов одного типа.
4. ``@Primary``. Определяет предпочтение, когда присутствует несколько bean-компонентов одного типа. Компонент, связанный с аннотацией @Primary, будет использоваться, если не указано иное.
5. ``@Transactional``. Делает методы над которыми висит транзакционными (обладающими свойствами транзакции).

<a name="spring-transactions"/>  

## Транзации Spring

Транзакцией называется набор связанных операций, все из которых должны быть выполнены корректно без ошибок. Если при выполнении одной из операций возникла ошибка, все остальные должны быть отменены. Прежде всего такой механизм применяется при работе с БД.

Транзации следует использовать для:
- Сохранения записи в таблицу
- Обновления записи в таблице
- Удаления записи из таблицы

Будет ли при вызове method2 из метода method1 создана новая транзакция?
```
public class MyServiceImpl {

    @Transactional
    public void method1() {
        //do something
        method2();
    }

    @Transactional(propagation=Propagation.REQUIRES_NEW)
    public void method2() {
        //do something
    }
}
```
Ответ: Для поддержки транзакций через аннотации используется Spring AOP, в момент вызова method1() на самом деле вызывается метод прокси объекта. Создается новая транзакция и далее происходит вызов method1() класса MyServiceImpl. А когда из method1() вызовем method2(), обращения к прокси нет, вызывается уже сразу метод нашего класса и, соответственно, никаких новых транзакций создаваться не будет.

Как сделать, чтобы создавалась новая транзакция в этом случае?
1. Использование TransactionManager
2. Self-inject класса и вызов метода через него (вызвать внутри одного метода другой через бин этого же класса). Прим.: Работает только для бинов со scope singleton, для prototype при старте приложения упадёт ошибка циклического внедрения бина самого в себя
3. Рефакторинг. Создание новой абстракции (например Facade), которая будет атомарно вызывать методы сервиса, помеченные @Transactional. Таким образом избегается перекрестный вызов транзакционных методов друг-другом.

Но в данном случае возникает проблема, когда в результате сбоя или ошибки может быть выполнена первая транзакция, а вторая нет. Для решения этой проблемы можно воспользоваться паттерном Transactional Outbox (общий подход для хранения завершенных транзакций).

<a name="spring-containers"/> 

## Spring контейнеры
Spring Framework предоставляет два наиболее фундаментальных и важных пакета, это пакеты org.springframework.beans и org.springframework.context. Код в этих пакетах обеспечивает основу для инверсии функций управления / внедрения зависимостей в Spring. Контейнеры Spring отвечают за создание объектов bean и внедрение их в классы.

**BeanFactory** - самый простой контейнер, обеспечивающий базовую поддержку DI, основан на интерфейсе org.springframework.beans.factory.BeanFactory. Наиболее распространенным классом реализации является XmlBeanFactory.

**ApplicationContext** - обертка, расположенная поверх BeanFactory, предоставляющая некоторые дополнительные возможности, например AOP, транзакции, безопасность, i18n, и т.п. ApplicationContext - это усовершенствованный контейнер, который расширяет функциональность BeanFactory в более ориентированном на фреймворк стиле. Чаще всего используются следующие реализации: ClassPathXmlApplicationContext, FileSystemXmlApplicationContext, WebXmlApplicationContext, AnnotationConfigWebApplicationContext и т.д.

<a name="bean-post-processor"/> 

## BeanFactoryPostProcessor и BeanPostProcessor

**BeanFactoryPostProcessor** позволяет настраивать определения bean-компонентов, а также работать с их конфигурационными метаданными ещё до фактического создания этих bean-компонентов. BeanFactoryPostProcessor создается и запускается перед BeanPostProcessor.

<details>
  <summary>Показать код</summary>
	
```
public interface BeanFactoryPostProcessor {
	public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory);
}
```
</details>

**BeanPostProcessor** - это интерфейс, который позволяет вмешиваться в процесс создания и настройки бинов. 
BeanPostProcessor предоставляет два метода, которые можно реализовать:
- postProcessBeforeInitialization: вызывается перед инициализацией бина, используется для изменения или настройки свойств бина перед его инициализацией.
- postProcessAfterInitialization: вызывается после инициализацией бина, используется для изменения или настройки свойств бина после его инициализации.

<details>
  <summary>Показать код</summary>

```
public class MyBeanPostProcessor implements BeanPostProcessor {

	@Override
	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		// Ваш код для изменения или настройки свойств бина перед его инициализацией
		return bean;
	}

	@Override
	public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
		// Ваш код для изменения или настройки свойств бина после его инициализации
		return bean;
	}
}
```
</details>

<a name="jvm-jdk-jre"/> 

## JVM, JDK, JRE
**JVM (Java Virtual Machine)** - виртуальная машина Java, исполняет байт-код, предварительно созданный из исходного текста Java-программы компилятором Java (javac). JVM обеспечивает платформо-независимый способ выполнения кода. Программисты могут писать код не задумываясь, как и где он будет выполняться.

**Байт-код** - это набор команд, который JVM применяет для запуска программы. Поскольку байт-код, сгенерированный для программы, не зависит от платформы, где она запущена, вы можете без проблем запускать свою программу на любой машине, на которой есть JVM для интерпретации байт-кода.

Байт-код - это просто результат компиляции класса Java. Файл .class на самом деле представляет собой набор инструкций байт-кода, в которые преобразуется код. Он нуждается в интерпретаторе, таком как JVM, чтобы понимать и выполнять инструкции.

**JRE (Java Runtime Environment)** - это минимальная реализация виртуальной машины, необходимая для исполнения Java приложений. Состоит из виртуальной машины и библиотек Java классов.

**JDK (Java Development Kit)** - это комплект разработчика приложений на языке Java, включающий в себя компилятор, стандартные библиотеки классов Java, примеры, документацию, различные утилиты и исполнительную систему JRE. 

<a name="annotations"/> 

## Аннотации
**Аннотации** - это форма метаданных. Они предоставляют информацию о программе, при том сами частью программы не являются.
```
//Создание аннотации
@interface ClassPreamble {
    String author();
    String date(); 
    int currentRevision() default 1; 
    String lastModified() default "N/A";
    String lastModifiedBy() default "N/A"; 
    // Можно использовать массив
    String[] reviewers(); 
 }

 //Использование
 @ClassPreamble ( 
    author = "John Doe", 
    date = "3/17/2002", 
    currentRevision = 6, 
    lastModified = "4/12/2004", 
    lastModifiedBy = "Jane Doe", 
    reviewers = {"Alice", "Bob", "Cindy"} 
) 
public class MyClass {
...
...
} 
```

<a name="abstract-class-vs-interface"/> 

## Абстрактный класс VS интерфейс
**Интерфейс** в языке программирования Java - это абстрактный тип, который используется для указания поведения, которое должны реализовывать классы.

**Абстрактный класс** - это класс, который может содержать методы, не имеющие реализации. Абстрактный класс создается с целью создания общего интерфейса между разными реализациями классов, которые будут производными от абстрактного класса. 
| Абстрактный класс | Интерфейс |
|:----------------|:---------|
| Для определения используется ключевое слово abstract | Для определения используется ключевое слово interface |
| Для наследования от абстрактного класса используется ключевое слово ``extends`` | Для реализации интерфейса используется ключевое слово ``implements`` |
| Разрешено как объявление, так и предоставление реализации методов по умолчанию | Разрешено только объявлять методы, но реализация их запрещена. Начиная с Java 8 стала допустима реализация методов посредством ключевого слова default |
| Может иметь как static, так и non-static поля (аналогичное относится и к final) | Любое поле интерфейса по умолчанию public static final (и иных иметь не может) |
| Члены абстрактного класса могут иметь любой модификатор доступа | Члены интерфейса могут быть объявлены как public (по умолчанию) и private (начиная с Java 9) |
| Может расширить (extends) любой другой класс и реализовать (implements) сколько угодно интерфейсов | Может расширить (extends) другой интерфейс |
| Связывает между собой и объединяет классы, имеющие близкую связь между собой | Один и тот же интерфейс могут реализовать классы, не имеющие ничего общего между собой |

_Прим_:  
Абстрактный класс не может быть final, т.к. нельзя создать объект абстрактного класса, а ключевое слово final предполагает, что класс не может иметь наследников.

_Прим_:  
Абстрактный класс не обязательно должен иметь абстрактные методы.

<a name="static_and_final"/> 

## Ключевые слова static и final
Для получения доступа к членам класса без создания экземпляра этого класса можно воспользоваться ключевым словом ``static``.
- **Статические переменные**
```
public class Car {

    public static int numberOfCars; //Общая переменная для всех экземпляров класса

    private String name;
    private String engine;  	 
  	 
    public Car(String name, String engine) {
        this.name = name;
        this.engine = engine;
        numberOfCars++;
    }
}
```
В Java сериализация позволяет сохранить текущее состояние объекта в поток байтов таким образом, чтобы его можно было передать, например, через сеть. Но, т.к. статические переменные относятся к классу, то они не могут быть сериализованы и просто игнорируются.
- **Статические методы**
```
public class Test {

    int x;

    //Общий метод для всех экземпляров
    public static void main(String[] args) {
        x = 0;
    }
}
```
_Прим:_
следует помнить, что из статического метода можно получить доступ только к статическим переменным или к другим статическим методам.
- **Статические блоки**
```
static {
}
```
Статические блоки применяют для инициализации статических переменных. Статический блок выполняется только один раз, когда класс загружается в память. Это происходит, если в коде запрашивается либо объект класса, либо статические члены этого класса.
- **Вложенный статический класс**
```
public class InnerClassExample {

    public String outerElement;
    private String outerPrivateElement;

    private void outerMethod() {

    }

    public static class MyStaticInnerClass{
        public void myFunction() { ... }
    }

    public class MyInnerClass {

        public void myAnotherFunction() { ... }
    }
    public static void main(String[] args) {
        //Вызов статического внутренего класса
        InnerClassExample.MyStaticInnerClass staticInner = new InnerClassExample.MyStaticInnerClass();
        staticInner.myFunction();
        
        /*Вызов внутреннего класса **/
        InnerClassExample.MyInnerClass innerClass = new InnerClassExample().new MyInnerClass();
        innerClass.myAnotherFunction();
    }
}
```

<a name="acid"/> 

## ACID
ACID - это стандарт того, какие гарантии должна давать база данных, чтобы поддерживать транзакции.

**Атомарность (atomicity)** - гарантирует, что каждая транзакция будет выполнена полностью или не будет выполнена совсем. Не допускаются промежуточные состояния.

**Согласованность (consistency)** - в результате работы транзакции данные будут допустимыми. Это вопрос не технологии, а бизнес-логики: например, если количество денег на счете не может быть отрицательным, логика транзакции должна проверять, не выйдет ли в результате отрицательных значений. 

**Изолированность (isolation)** - гарантия того, что параллельные транзакции не будут оказывать влияния на результат других транзакций.

**Долговечность (durability)** - изменения, получившиеся в результате транзакции, должны оставаться сохраненными вне зависимости от каких-либо сбоев. Иначе говоря, если пользователь получил сигнал о завершении транзакции, он может быть уверен, что данные сохранены.

Изолированность достигается за счёт:  
**1. Версионирование (snapshot)** означает, что транзакции будут работать со своей копией данных, не влияя друг на друга, но впоследствии несколько изменённых копий надо будет как-то слить в одну. Строгость версионирования регулирует моменты (когда) и размеры (сколько данных копировать) этих копий.  

**2. Блокирование (lock)** означает, что одна транзакция будет ждать другую, чтобы избежать побочных эффектов, в зависимости от строгости уровней изоляции этих транзакций. Различные виды блокировок обеспечивают более гранулярное блокирование, например, только по строкам, или только на небольшой кусочек транзакции, а не на всю.

Уровни изолированности БД:
- READ_UNCOMMITTED (Каждая транзакция видит незафиксированные изменения другой транзакции). Могут происходить грязные чтения, неповторяемые чтения, фантомные чтения и потерянное обновление.
- READ_COMMITTED (Параллельно исполняющиеся транзакции видят только зафиксированные изменения из других транзакций). Грязные чтения предотвращены, но могут возникать неповторяющиеся чтения, фантомные чтения и потерянное обновление.
- REPEATABLE_READ (Уровень, позволяющий предотвратить феномен неповторяющегося чтения. Т.е. мы не видим в исполняющейся транзакции измененные и удаленные записи другой транзакцией. Но все еще видим вставленные записи из другой транзакции). Грязные чтения, неповторяющиеся чтения и потерянное обновление предотвращены, но могут возникать фантомные чтения.
- SERIALIZABLE Транзакции полностью изолированы. Исключено влияние одной транзакции на другую в момент выполнения.

<a name="collections"/> 

## Коллекции

**Иерархия коллекций Java:**  

![image](https://user-images.githubusercontent.com/73114969/195570339-3f7f837a-db2b-4b74-a07e-218521cde185.png)

**Описание интерфейсов коллекций:**  

**Iterable** - позволяет пользователям последовательно перебирать элементы из коллекции (Collection наследует этот интерфейс).

**Set** - это неупорядоченное множество уникальных элементов.  

**List** - упорядоченный список, в котором у каждого элемента есть индекс. Дубликаты значений допускаются.

**Queue** - очередь. В таком списке элементы можно добавлять только в хвост, а удалять — только из начала. Так реализуется концепция FIFO (first in, first out) - «первым пришёл — первым ушёл».

**Deque** - двунаправленная очередь. По сути может выступать и как очередь, и как стек. Это значит, что элементы можно добавлять как в её начало, так и в конец. То же относится к удалению.

**Map** - состоит из пар «ключ-значение». Ключи уникальны, а значения могут повторяться. Порядок элементов не гарантирован. Map позволяет искать объекты (значения) по ключу.

**Описание конкретных реализаций интерфейсов:**

**ArrayList** - реализует интерфейс List и строится на базе обычного массива. Если при создании не указать размерность, то под значения выделяется 10 ячеек. При попытке добавить элемент, для которого места уже нет, массив автоматически расширяется. 

**LinkedList** - реализует одновременно List и Deque. Это список, в котором у каждого элемента есть ссылка на предыдущий и следующий элементы. Благодаря этому добавление и удаление элементов выполняется быстро - времязатраты не зависят от размера списка, так как элементы при этих операциях не сдвигаются: просто перестраиваются ссылки.

**ArrayDeque** — это реализация двунаправленной очереди в виде массива с переменным числом элементов. Новые значения можно добавлять в начало или конец списка, и удалять оттуда же.

_Прим:_  
*Когда выгоднее использовать LinkedList, а когда — ArrayList?
Если добавлять и удалять элементы с произвольными индексами в списке нужно чаще, чем итерироваться по нему, то лучше LinkedList. В остальных случаях — ArrayList.*

**PriorityQueue** — упорядоченная очередь. По умолчанию элементы добавляются в естественном порядке: числа по возрастанию, строки по алфавиту и так далее, либо алгоритм сравнения задаёт разработчик.

**HashSet** - использует для хранения данных в хеш-таблице. Это значит, что при манипуляциях с элементами используется хеш-функция — hashCode() в Java.

**HashMap** - состоит из массива односвязных списков - бакетов, размером 16. При добавлении пары K-V в HashMap высчитывается hashcode ключа key.hashcode() и побитово умножается на (n-1), где n - длинна внутреннего массива. Получается число от 0 до n-1. Данная пара K-V помещается в ячейку соответствующей, числу, полученному в предыдущей операции. Со всеми следующими парами K-V работа аналогичная. Если элементов становится слишком много, в HashMap выделяется еще один массив размерностью 16 (Или каждый бакет становится красно-черным деревом).

**LinkedHashMap** - расширяет возможности HashMap тем, что позволяет итерироваться по элементам в порядке их добавления. Как и в LinkedList, здесь каждая пара-значение содержит ссылку на предыдущий и последующий элементы.

**TreeMap** - строится тоже на базе красно-чёрного дерева. Элементы здесь упорядочены (в естественном или заданном при создании порядке) в каждый момент времени.

Коллекции, где не допускаются null-элементы:  
- TreeMap
- TreeSet
- ArrayDeque

<a name="garbage-collector"/> 

## Сборщик мусора (Garbage Collector)

JVM обычно запускает сборщик мусора при низком уровне свободной памяти. Но работа сборщика мусора не гарантирует, что всегда будет оставаться достаточно свободной памяти.

Если памяти недостаточно даже после восстановления, JVM генерирует исключение OutOfMemoryError.

Задачи GC:  
**1. Reference counting** - учет ссылок. Каждый объект имеет счетчик (количество указывающих на него ссылок). когда счетчик = 0 объект считается мусором. Из-за невозможности работы с циклическими зависимостями данный подход не используется.  
**2. Tracing – трассировка** - до «живого» объекта можно добраться из корневых точек (GC Root). Всё, что доступно из «живого» объекта, также является «живым». Если представить все объекты и ссылки между ними как дерево, то необходимо пройти от корневых узлов GC Roots по всем узлам. При этом узлы, до которых нельзя добраться, являются мусором.

GC Root (корневые узлы):
- Основной Java поток - поток, который выполняет main.
- Локальные переменные в основном методе - параметры main метода и локальные переменные внутри main метода.
- Статические переменные основного класса - статические переменные основного класса, внутри которого находится main метод.


Сборщики мусора в Java реализуют стратегию сбора мусора поколений, которая классифицирует объекты по возрасту:

**1. Молодое поколение (Young Generation)**  
Вновь созданные объекты начинаются в Young Generation. Оно подразделяется на Eden Space, где начинаются все новые объекты, и два пространства Survivor , где объекты перемещаются из Eden после сохранения (surviving) в одном цикле сборки мусора. Они вызывают повторную сборку мусора, когда объекты собираются сборщиком мусора из Young Generation.

**2. Старшее поколение (Old Generation)**  
Объекты-долгожители в конечном итоге переходят из молодого поколения в старшее. После незначительной сборки мусора, когда устаревшие объекты достигают определенного порога возраста (по умолчанию порог современных JVM установлен на 15 циклов сборки мусора), они вместе с объектами-долгожителями переходят из молодого поколения в старое. 

**3. Постоянное поколение (Permanent Generation)**  
В PermGen виртуальная машина хранит метаданные загруженных классов. Также здесь находятся всё статическое содержимое приложения, переменные примитивных типов и ссылки на статические объекты.

Начиная с Java 8, на смену пространству постоянного поколения (PermGen) приходит пространство памяти MetaSpace. Реализация отличается от PermGen — это пространство кучи теперь изменяется автоматически.
Это позволяет избежать проблемы нехватки памяти у приложений, которая возникает из-за ограниченного размера пространства PermGen в куче.

<a name="soap"/> 

## SOAP

SOAP – это сокращение от Simple Object Access Protocol. Это протокол обмена сообщениями на основе XML для обмена информацией между компьютерами. SOAP является приложением спецификации XML.

<a name="rest"/> 

## REST
REST - сокращение от английского Representational State Transfer - передача состояния представления. Это архитектурный стиль взаимодействия компонентов распределенной системы в компьютерной сети.  

Чтобы система считалась RESTful, она должна “вписываться” в шесть REST ограничений: 
- Приведение архитектуры к модели клиент-сервер. Должно быть четкое разграничение между клиентом и сервером.
- Отсутствие сохранения состояния. Все клиент-серверные операции должны быть без сохранения состояния. Любое необходимое управление состоянием должно осуществляться на клиенте, а не на сервере.
- Кэширование. Все ресурсы должны разрешать кэширование, если явно не указано, что оно невозможно.
- Единообразие интерфейса. Ресурсы должны быть однозначно идентифицированы посредством одного URL-адреса и только с помощью базовых методов сетевого протокола (DELETE, PUT, GET, HTTP).
- Многоуровневая система. REST API допускает архитектуру, которая состоит из нескольких уровней серверов.
- Код по требованию. В большинстве случаев сервер отправляет обратно статические представления ресурсов в формате XML или JSON. Однако при необходимости серверы могут отправлять исполняемый код непосредственно клиенту.

Преимущества, которые дает REST:
- производительность (за счёт использования кэша);
- масштабируемость;
- прозрачность системы взаимодействия;
- простота интерфейсов;
- портативность компонентов;
- лёгкость внесения изменений;
- способность эволюционировать, приспосабливаясь к новым требованиям.

<a name="async-sync-communication"/> 

## Асинхронное/синхронное общение
Чтобы обеспечить взаимодействие между микросервисами, используют два распространенных способа: синхронный и асинхронный. В первом случае вызывающая сторона ожидает ответа перед отправкой сообщения, работая как протокол REST (Representational state transfer) поверх HTTP. Во втором — сообщения отправляются, не ожидая ответа. Такой вариант подходит для распределенных систем и обычно нуждается в брокере для управления сообщениями.

<a name="kafka"/> 

## Kafka
**Kafka** — гибрид распределённой базы данных и брокера сообщений.

Краткая инфа:
- Модель publisher(публикует сообщения)-subscriber(читает сообщения)
- У каждого подписчика есть свой offset - номер первого непрочитанного сообщения
- Подписчики, которые читают сообща, находятся в одной consumer-группе имеют общие offset'ы
- Сообщения распределяются по партициям по ключу партицирования. От каждого сообщения считается hash-функция и высчитывается остаток от деления на число партиций
- Для отказоустойчивости используются брокеры, которые содержат в себе копии сообщений. Обычно брокера 3
- Удаляются сообщения согласно 2м стратегиям: по времени (default- неделя) или по размеру очереди
- Чтение обычно происходит пачками. Настройка ``max.pool.records``. После изучения новой пачки фиксируется новый offset.
- Время чтения одной пачки сообщений настраивается через ``max.pool.intervals.ms``. Если consumer не успевает прочитать сообщения за отведенное время, его отстраняют, заменяя следующим, группу перебалансируют.

Кафку применяют для:
- Асинхронное взаимодействие. Нам не важен ответ; Последующее действие не зависит от результата асинхронной операции
- Амортизация нагрузки. Отправителю не нужно ждать, когда принимающая сторона обработает всю инфу.
- Потоковая обработка данных. Возможность обрабатывать большое количество сообщений в секунду.
- Репликация данных. Мастер-система пушит в кафку каждое изменение данных, Системы считывают изменения и актуализируют собственные копии мастер-данных.
- Event-driven architecture.

Отличие подхода "очереди" в RabbitMQ (ещё один брокер сообщений) и "топиков" в Kafka:
- К очереди подключается только один консьюмер, считывает последовательно и сообщения после этого пропадают.  
- К топику можно подключить сколько угодно консьюмеров, каждый из консьюмеров будет читать тот offset, на которм он остановился. Сообщения после считывания не пропадают (есть срок годности).

В отличие от большинства систем, очередь сообщений в Kafka является постоянной. Отправленные данные хранятся до тех пор, пока не истечет указанные период. Сообщения не удаляются после получения, их можно перечитывать. 

В RabbitMQ сообщение хранится до тех пор, пока принимающее приложение не получит его из очереди. Как только подписчик отмечает, что сообщение получено, оно удаляется. 

<a name="exceptions"/> 

## Exceptions (Исключения)
Исключение - любая ошибка, которая возникает в ходе выполнения программы.

Иерархия исключений:

![image](https://user-images.githubusercontent.com/73114969/195692746-53b486c4-d64e-44c2-b366-295a92b8501b.png)


**Error** - ошибки, возникающие при выполнении программы в результате сбоя работы JVM, переполнения памяти или сбоя системы. Обычно они свидетельствуют о серьезных проблемах, устранить которые программными средствами невозможно.
**Exceptions** - исключения, которые являются результатом проблем в программе и могут быть обработаны и являются предсказуемыми.

Все исключительные ситуации делятся на «проверяемые» (checked) и «непроверяемые» (unchecked).
- Проверяемые исключения должны обязательно обрабатываться. Обработка этих исключений првоеряется на этапе компиляции.
- Непроверяыемые исключения - это исключения времени выполнения (наследуются от RuntimeException). Компилятор не будет от вас требовать обработки непроверяемых исключений.

Синтаксис:  
- try – определяет блок кода, в котором может произойти исключение;
- catch – определяет блок кода, в котором происходит обработка исключения;
- finally – определяет блок кода, который является необязательным, но при его наличии выполняется в любом случае независимо от результатов выполнения блока try;
- throw - принудительно генерирует исключение;
- throws - указывается в сигнатуре метода и говорит о том, что метод может выбросить исключение.

Блок finally{} не выполнится в следующих случаях:
- В самом блоке finally вылетает ошибка
- Если вызывается метод System.exit()
- Операционная система завершит работу JVM
- Если блок finally будет выполняться потоком демона, а все остальные потоки не демоны завершат свое выполнение

Использование try with resources:
```
try(BufferedWriter writer = new BufferedWriter(new FileWriter(fileName))){
    writer.write(str); 
catch(IOException e){
	...	
}
```
В try создаем некие сущности, которые должны поддерживать интерфейс AutoClosable. По окончанию блока try, не зависимо от того было ли исключение или нет, эти сущности закроются. (исп. для чтения потоков или соединения с БД).

<a name="o-notation"/> 

## Алгоритмическая сложность(O-нотация)
Сложность алгоритмов обычно оценивают по времени выполнения или по используемой памяти.
- O(1) – константная сложность
- O(n) - линейная сложность
- O(log n) - логарифмическая сложность
- O(n*log(n)) - квазилинейная сложность
- O(n^2) - квадратичная сложность
- O(2^n) - экспоненциальная сложность.

Алгоритмическая сложность структур:

![image](https://user-images.githubusercontent.com/73114969/195703162-84b99448-d7f8-426c-854b-89ff8d0bfb40.png)

Алгоритмическая сложность сортировок:

![image](https://user-images.githubusercontent.com/73114969/195703400-31d1c64c-c7af-4a0d-94be-8dba63a6b6c2.png)

<a name="immutability"/> 

## Иммутабельность в Java
Иммутабельный (неизменяемый, immutable) класс — это класс, который после инициализации не может изменить свое состояние. То есть если в коде есть ссылка на экземпляр иммутабельного класса, то любые изменения в нем приводят к созданию нового экземпляра.

Чтобы класс был иммутабельным, он должен соответствовать следующим требованиям:

- должен быть объявлен как final, чтобы от него нельзя было наследоваться. Иначе дочерние классы могут нарушить иммутабельность.
- все поля класса должны быть приватными в соответствии с принципами инкапсуляции.
- для корректного создания экземпляра в нем должны быть параметризованные конструкторы, через которые осуществляется первоначальная инициализация полей класса.
- для исключения возможности изменения состояния после инстанцирования, в классе не должно быть сеттеров.
- для полей-коллекций необходимо делать глубокие копии, чтобы гарантировать их неизменность.

Иммутабельные классы в Java:
- String
- Все классы-обертки примитивных типов
- Объекты класса java.lang.StackTraceElement

<a name="heap-stack"/> 

## Heap и Stack память

**Java Heap (куча)** используется Java Runtime для выделения памяти под объекты и JRE классы. Создание нового объекта также происходит в куче. Здесь работает сборщик мусора: освобождает память путем удаления объектов, на которые нет каких-либо ссылок. 

**Stack память** - стековая память в Java используется для распределения статической памяти и выполнения потока. Он содержит примитивные значения, специфичные для метода, и ссылки на объекты в куче, на которые ссылается метод. Всякий раз, когда вызывается метод, в памяти стека создается новый блок, который содержит примитивы и ссылки на другие объекты в методе. Как только метод заканчивает работу, блок также перестает использоваться, тем самым предоставляя доступ для следующего метода.

Разница между кучей и стеком:
- Куча используется всеми частями приложения в то время как стек используется только одним потоком исполнения программы.
- Всякий раз, когда создается объект, он всегда хранится в куче, а в памяти стека содержится ссылка на него. Память стека содержит только локальные переменные примитивных типов и ссылки на объекты в куче.
- Объекты в куче доступны с любой точки программы, в то время как стековая память не может быть доступна для других потоков.
- Стековая память существует лишь какое-то время работы программы, а память в куче живет с самого начала до конца работы программы.
- Мы можем использовать -Xms и -Xmx опции JVM, чтобы определить начальный и максимальный размер памяти в куче. Для стека определить размер памяти можно с помощью опции -Xss .
- Если память стека полностью занята, то Java Runtime бросает java.lang.StackOverflowError, а если память кучи заполнена, то бросается исключение java.lang.OutOfMemoryError: Java Heap Space.
- Размер памяти стека намного меньше памяти в куче. Из-за простоты распределения памяти (LIFO), стековая память работает намного быстрее кучи.

<a name="object-class-and-methods"/> 

## Класс Object и его методы

``toString()`` - возвращает символьную строку, описывающую объект.

``clone()`` - создает новый объект, не отличающийся от клонируемого.  

``finalize()`` - вызывается перед удалением неиспользуемого объекта.

``getClass()`` - получает класс объекта во время выполнения.

``notify()`` - возобновляет исполнение потока, ожидающего вызывающего объекта.

``notifyAll()`` - возобновляет исполнение всех потоков, ожидающих вызывающего объекта.

``wait()`` - ожидает другого потока исполнения.

``wait(long timeout)`` - ожидает другого потока исполнения.

``wait(long timeout, int nanos)`` - ожидает другого потока исполнения.

``equals(Object obj)`` - гарантирует: если ``o1.equals(o2)`` вернул ``true``, то объекты равны. Если ``false``, то элементы точно не равны друг другу.

``hashCode()`` - гарантирует что если у 2х объектов разные хэшкоды - эти объекты точно разные, а если хэшкоды равны то либо объекты равны, либо произошла коллизия.

При вызове o1.equals(o2) сначала сравниваются их хэшкоды, если хеши не равны, выдаётся false, если равны, то вызывается метод equals(), который работает долго, но выдаёт точный ответ (сравнивая объекты по ссылкам).

Стоит отметить, что для корректной работы, при создании собственного класса, всегда нужно переопределять методы equals() и hasCode(), придерживаясь следующих правил:
- Рефлексивность - для любого заданного значения x, выражение x.equals(x) должно возвращать true. (Заданного — имеется в виду такого, что x != null)
- Симметричность - для любых заданных значений x и y, x.equals(y) должно возвращать true только в том случае, когда y.equals(x) возвращает true.
- Транзитивность - для любых заданных значений x, y и z, если x.equals(y) возвращает true и y.equals(z) возвращает true, x.equals(z) должно вернуть значение true.
- Согласованность - для любых заданных значений x и y повторный вызов x.equals(y) будет возвращать значение предыдущего вызова этого метода при условии, что поля, используемые для сравнения этих двух объектов, не изменялись между вызовами.
- Сравнение null - для любого заданного значения x вызов x.equals(null) должен возвращать false.

<a name="io-streams"/> 

## Потоки IO
IO API – (Input & Output) в первую очередь это Java API, которые облегчают работу с потоками. В java.io существуют так называемые потоки ввода и вывода (InputStream and OutputStream).

**Базовые:**
- InputStream / OutputStream - абстрактный класс, определяющий потоковый байтовый ввод/вывод
- Reader / Writer - Символьные потоки имеют два основных абстрактных класса Reader и Writer, управляющие потоками символов Unicode.
- InputStreamReader / OutputStreamWriter Входной/выдодной поток, транслирующий байты в символы

**Массивы:**
- ByteArrayInputStream / ByteArrayOutputStream - использует байтовый массив в потоке.
- CharArrayReader / CharArrayWriter - читает/пишет из символьного массива.

**Files:**

- FileInputStream / FileOutputStream - Чтение/Отправка данных в файл на диске. Реализация класса OutputStream
- RandomAccessFile / RandomAccessFile - Чтение/запись файлов с произвольным доступом. метод seek() позволяет переместиться к определенной позиции и изменить хранящееся там значение. При использовании RandomAccessFile необходимо знать структуру файла. Класс RandomAccessFile содержит методы для чтения и записи примитивов и строк UTF-8. RandomAccessFile может открываться в режиме чтения ("r") или чтения/записи ("rw"). Также есть режим "rws", когда файл открывается для операций чтения-записи и каждое изменение данных файла немедленно записывается на физическое устройство.
- FileReader / FileWriter FileWriter записывает данные в файл. При вводе/выводе практически всегда применяется буферизация, поэтому используется BufferedWriter.
Когда данные входного потока исчерпываются, метод readLine() возвращает null. Для потока явно вызывается метод close(); если не вызвать его для всех выходных файловых потоков, в буферах могут остаться данные, и файл получится неполным

**Буферизация**

- BufferedInputStream / BufferedOutputStream - буферизируемый поток. Буферы вывода нужно для повышения производительности
- BufferedReader / BufferedWriter

<a name="nested-internal-classes"/> 

## Вложенные и внутренние классы

**1. Вложенный статический**

```
class OuterClass {
  ...
  static class StaticNestedClass {
    ...
  }
}

//Использование
OuterClass.StaticNestedClass nestedObject = new OuterClass.StaticNestedClass();
```
В случае с java вложенными статическими классами вы не можете напрямую обращаться к методам родительского класса или нестатическим полям. Для решения  этой задачи необходимо создать экземпляр и работать со ссылкой. Данная конструкция схожа с тем, как осуществляется взаимодействие с классами извне.

**2. Обычный внутренний**

```
class Outer {
  int x1 = 3;
  class Inner {
    void display() {
      System.out.println ("x1 = " + String.valueOf(x1));
    }
  }
}
```
Внутренний класс не имеет никаких ограничений, может обращаться ко всем переменным и методам старшего класса.

**3. Локальный**

Локальные классы необходимо объявлять внутри методов, вне их использовать их нельзя. Кроме того, они могут обращаться ко всем внешним переменным, но только если те являются final.
```
public void print() {

  class Logger {
    String name;
  }

//Использование
Logger logger = new Logger();
}
```

**4. Анонимный**

Анонимные внутренние классы java аналогичны локальным, только не имеют имени. Они также имеет все указанные ограничения, плюс для них нельзя создать конструктор.
```
AnonymousInner an_inner = new AnonymousInner() {
   public void my_method() {
      ........
      ........
   }   
};
```

<a name="data-structures"/> 

## Структуры данных

**Массив** - структура данных, хранящая набор значений (элементов массива), идентифицируемых по индексу или набору индексов.  

**Список** - динамическая линейная структура данных, хранящая конечную последовательность элементов, порядок которых определяется с помощью ссылок.

**Стек** - структура данных позволяет добавлять и удалять элементы только из начала.

**Очередь** - структура данных позволяет добавлять данные в конец, а извлекать из начала.

**Карта** - данные здесь хранятся в паре «ключ/значение», причем каждый ключ уникален, а вот значения могут повторяться.

**Дерево** - это структура, данные в которой лежат в узлах. У каждого узла могут быть один или несколько дочерних и только один родитель, то есть они расходятся, как ветви дерева.

**Граф** - это более общий случай дерева. Иногда деревья называют ациклическими графами. В отличие от дерева в графе возможны циклы, то есть «ребёнок» может быть «родителем» для того же элемента. Рёбра тоже могут нести смысловую нагрузку, то есть нужно сохранять их значения.

<a name="stream-api"/> 

## Stream Api Java

**Stream API** - это способ работать со структурами данных Java, чаще всего коллекциями, в стиле функциональных языков программирования.

Операторы можно разделить на две группы:
- Промежуточные (“intermediate”, ещё называют “lazy”) — обрабатывают поступающие элементы и возвращают стрим. Промежуточных операторов в цепочке обработки элементов может быть много.
- Терминальные (“terminal”, ещё называют “eager”) — обрабатывают элементы и завершают работу стрима, так что терминальный оператор в цепочке может быть только один.

Промежуточные:
- map - преобразование исходного элемента
- filter - фильтрация
- peek - доступ к элементу, не меняя его
- distinct - удаление дубликатов
- sorted - сортировка
- limit - ограничение по количеству элементов
- skip - пропуск первых элементов
- flatMap - преобразует каждый элемент в Stream, объединяет Stream всех элементов в один и передает его следующему оператору.

Терминальные:
- forEach
- count - возвращает количество элементов стрима
- collect - метод собирает все элементы в список, множество или другую коллекцию, сгруппировывает элементы по какому-нибудь критерию
- reduce - преобразует все элементы стрима в один объект (например когда надо посчитать сумму)
- min/max
... ДОПИСАТЬ...

<a name="db"/> 

## БД

**Реляционная база данных (БД)** — это совокупность связанных между собой двумерных таблиц, в которых хранится информация об объектах.

**Ограничения:**
- NOT NULL — колонка не может иметь нулевое значение
- DEFAULT — значение колонки по умолчанию
- UNIQUE — все значения колонки должны быть уникальными
- PRIMARY KEY — первичный или основной ключ, уникальный идентификатор записи в текущей таблице
- FOREIGN KEY — внешний ключ, уникальный идентификатор записи в другой таблице (таблице, связанной с текущей)
- CHECK — все значения в колонке должны удовлетворять определенному условию
- INDEX — быстрая запись и извлечение данных

**Команды**
- CREATE - создает новую таблицу, представление таблицы или другой объект в БД
- ALTER - модифицирует существующий в БД объект, такой как таблица
- DROP - удаляет существующую таблицу, представление таблицы или другой объект в БД
- SELECT - извлекает записи из одной или нескольких таблиц
- INSERT - создает записи
- UPDATE - модифицирует записи
- DELETE - удаляет записи
- DISTINCT - отфильтровывает повторяющиеся значения и возвращает строки указанного столбца
- WHERE - используется для фильтрации записей/строк
- ORDER BY - используется для сортировки набора результатов в порядке возрастания (ASC - по умолчанию) или убывания (DESC)
- INNER JOIN - возвращает записи, имеющие совпадающее значение в обеих таблицах
- LEFT JOIN - возвращает записи из левой таблицы, даже если такие записи отсутствуют в правой таблице
- RIGHT JOIN - возвращает записи из правой таблицы, даже если такие записи отсутствуют в левой таблице
- FULL JOIN - возвращает все записи объединяемых таблиц
- UNION - используется для объединения результирующего набора из двух или более заявлений SELECT, каждый оператор SELECT в UNION должен иметь одинаковое количество столбцов, столбцы также должны иметь схожие типы данных и располагаться в том же порядке

**Агрегатные функции:**
- COUNT - считает количество записей в колонке
- SUM - складывает содержимое значений колонки
- MIN - указывает на минимальное значение в колонке
- MAX - указывает на максимальное значение в колонке
- AVG - считает среднее значение в колонке
- ROUND - округляет значение в колонке

Для работы с инструкциями, которые содержат агрегатные функции, есть специальные операторы:
- GROUP BY - группирует выходные значения для колонок, к которым применили агрегатную функцию
- HAVING - работает как WHERE, но может применяться к агрегатным функциям

**Логические операторы:**
- ALL - сравнивает все значения
- AND - объединяет условия (все условия должны совпадать)
- ANY - сравнивает одно значение с другим, если последнее совпадает с условием
- BETWEEN - проверяет вхождение значения в диапазон от минимального до максимального
- EXISTS - определяет наличие строки, соответствующей определенному критерию
- IN - выполняет поиск значения в списке значений
- LIKE - сравнивает значение с похожими с помощью операторов подстановки
- NOT - инвертирует (меняет на противоположное) смысл других логических операторов, например, NOT EXISTS, NOT IN и т.д.
- OR - комбинирует условия (одно из условий должно совпадать)
- IS NULL - определяет, является ли значение нулевым
- UNIQUE - определяет уникальность строки

**Нормализация** - устранение избыточности таблиц

**Подзапрос** - это запрос, вложенный в другой запрос

**Представление (VIEW)** - объект базы данных, являющийся результатом выполнения запроса к базе данных, определенного с помощью оператора SELECT, в момент обращения к представлению.

**Работы** – это набор определенных действий (например, SQL запросов), которые могут выполняться сервером автоматически в определенное время с помощью планировщика (Schedule) или запускаться администратором вручную.

**Партицирование** - функция, которая позволяет разбивать большие таблицы на логические части по выбранным критериям, благодаря чему улучшается производительность базы данных.

**Индекс** - это структура данных, которая повышает скорость операций поиска данных в таблице базы данных за счет дополнительных операций записи и места для хранения для поддержания структуры данных индекса.

Проблемы, возникающие при работе с индексами: 
 - Индексы могут разрастаться до больших размеров
 - При update исходной таблицы тратится много времени на модификацию индексов, если их много

<a name="assemblers"/> 

## Сборщики/maven

Сборщики позволяют:
- загрузить зависимые библиотеки для вашего проекта из сети (репозитория);
- скомпилировать классы модуля или всего проекта;
- сгенерировать дополнительные файлы: SQL-скрипты, XML-конфиги и т.п.;
- удалять/создавать директории и копировать в них указанные файлы;
- упаковка скомпилированных классов проекта в архивы различных форматов: zip, rar, rpm, jar, ear, war и др.;
- компиляция и запуск модульных тестов (unit-test) вашего проекта с результатами выполнения тестов и расчетом процента покрытия;
- установка (deploy) файлов проекта на удаленный сервер;
- генерация документации и отчетов.

Основные команды maven:
- compile - компилируются файлы с исходным кодом.
- clean - удаляются все скомпилированные файлы из каталога target (место, в котором сохраняются готовые артефакты).
- package - упаковываются скомпилированные файлы (в jar, war и т.д. архив).
- install - пакет помещается в локальный репозиторий. Теперь он может использоваться другими проектами как внешняя библиотека.
- test — запускаются тесты.

Способы сборки: jar/war/flat/fat ???

Элементы, используемые в создании файла pom.xml:
- project - проект является корневым элементом файла pom.xml.
- modelVersion - означает версию модели POM, с которой вы работаете.
- groupId - подразумевает идентификатор группы проекта. Он уникален, и чаще всего вы будете применять идентификатор группы, связанный с именем корневого пакета Java.
- artifactId - используется для предоставления названия проекта, который вы собираете.
- version - этот элемент состоит из номера версии проекта. Если ваш проект был выпущен в различных версиях, тогда удобно представить версию вашего проекта.

<a name="ci-cd"/>

## CI/CD

Непрерывная интеграция (CI) — это методология разработки и набор практик, при которых в код вносятся небольшие изменения с частыми коммитами. И поскольку большинство современных приложений разрабатываются с использованием различных платформ и инструментов, то появляется необходимость в механизме интеграции и тестировании вносимых изменений.

CI/CD включает в себя:
- обеспечение последовательного и автоматизированного способа сборки, упаковки и тестирования продуктов или приложений;
- автоматизация развертывания в разных окружениях;
- сведение к минимуму ошибок и проблем.

<a name="kotlin"/>

## Kotlin

**Отличия Kotlin от Java:**

1. Kotlin защищен от NullPointerException. В отличие от Java, в Kotlin по умолчанию все типы являются non-nullable, то есть не могут принимать значение null. Присвоение или возврат null приведет к ошибке компиляции. Чтобы присвоить переменной значение null, в Kotlin необходимо явно пометить эту переменную как nullable.
```
val number: Int? = null //Nullable type
val name: String = null //Error because not possible to assign a null value
```
Nullable-типы используются с оператором безопасного вызова.
```
name?.getLength()
```
Таким образом, даже если name примет значение null, все выражение будет эквивалентно null без возникновения NullPointerException.
2. В отличие от Java, по умолчанию классы в Kotlin являются финальными (final), поэтому, чтобы разрешить наследование от класса, его следует пометить ключевым словом open. Чтобы разрешить переопределение метода, его необходимо явно пометить как open.
3. В Kotlin все, что не имеет модификаторов доступа, по умолчанию является public. Мы можем явно прописать public в определении, но это не обязательно.

Модификаторы в Kotlin:
- private: члены класса с этим модификатором видны только в рамках своего класса
- protected: члены класса с этим модификатором видны в классе, в котором они определены, и в классах-наследниках
- internal: классы, объекты, интерфейсы, функции, свойства, конструкторы с этим модификатором видны в любой части модуля, в котором они определены. 
- public: классы, функции, свойства, объекты, интерфейсы с этим модификатором видны в любой части программы. 

4. Изменяемым (mutable) и неизменяемым (immutable) типами в Kotlin являются var и val.
5. В числовых литералах разрешается использовать символы подчеркивания.
```
val creditCardNumber = 1234_5678_9012_3456L
```
6. Нельзя сравнивать типы разной величины.
```
val a: Int = 10; val b: Long = 10L
print(a == b) // Ошибка в Kotlin: сравнение невозможно. В Java возвращается true.
```
7. Имена примитивных типов данных в Kotlin начинаются с заглавной буквы.
8. Тип List по умолчанию в Kotlin является неизменяемым, поэтому методы add() или remove() работают не так, как в Java.
```
val lst = listOf<Int>(10, 20, 30, 40, 50)
lst.add(60) //Ошибка
val lst2 = mutableListOf<Int>(10, 20, 30, 40, 50) //то же самое, что ArrayList<Int>
// val для mutableList? Да, потому что нового присваивания не происходит, только изменение содержимого.
lst2.add(60) //OK
lst2 += 70 //тоже OK
```
Оперировать списком в языке Kotlin можно с помощью функций take и drop.
```
val nums = listOf(0,1,2,3,4,5,6,7)
nums.take(3) // [0,1,2]
nums.drop(3) // [3,4,5,6,7]
```
9. В Kotlin доступны два вида конструкторов. Один из них прописывается после имени класса и называется первичным конструктором, а второй прописывается в теле класса и называется вторичным конструктором. В классе могут быть один первичный конструктор и несколько вторичных. Первичный конструктор не может содержать код. Код инициализации можно поместить в блок init. Вторичный конструктор должен расширять поведение первичного конструктора.
10. Kotlin позволяет разработчикам расширять класс, добавляя новую функциональность при помощи функций-расширений. По сути, функция-расширение — это функция, которая является членом класса, но определена за его пределами.
```
fun String.countSpaces(): Int {
return this.count { c -> c == ‘ ‘ }
}
```
11. В языке Kotlin функция, которая может принимать в качестве параметра функцию или лямбда-выражение или же может возвращать функцию, называется функцией высшего порядка (higher-order function).
```
// лямбда-выражение
var lambda = {a: Int , b: Int -> a + b }
//функция высшего порядка
fun highfun( lmbd: (Int, Int) -> Unit) { // принимает лямбда-выражение как параметр, ничего не возвращает
var result = lmbd(2,4) // вызывает лямбда-выражение, передавая ему параметры
println(“Сумма двух чисел равна $result”)
}
fun main() {
highfun(lambda) //лямбда-выражение передается как параметр
}
```
12. В больших проектах, как правило, используется несколько классов, предназначенных исключительно для хранения данных. Разработчику на Java приходится писать много стандартного, но часто встречающегося кода (так называемый шаблонный код или boilerplate), data-классы в Kotlin позволяют избежать этих дополнительных усилий.В Java-классе для этой цели должны присутствовать геттеры и сеттеры, функции Hashcode(), toString() и equals(). Эквивалентом в Kotlin будет:
```
data class Person(var name: String, var surname: String, var id: String)
```
13. Как только мы объявляем переменную static, она загружается в память во время компиляции, то есть доступна только одна ее копия. Ключевое слово static делает компонент частью класса, не связанной с объектом этого класса. В Java все должно объявляться внутри класса. Но в Kotlin все иначе. Компоненты могут объявляться за пределами класса, и это автоматически делает их статическими. Поэтому нам не требуется ключевое слово static. В Java статические члены обрабатываются не так, как члены-объекты. Это означает, что для статических членов нам недоступны такие вещи, как реализация интерфейса, помещение экземпляра в ассоциативный список (map) или передача его в качестве параметра методу, который принимает объект. В Kotlin static не является ключевым словом и вместо статических членов используются объекты-компаньоны, позволяющие преодолеть вышеуказанные ограничения.
14. В Java существует множество решений для асинхронной работы: RxJava, AsyncTask (уже официально не поддерживается), обработчики, обратные вызовы. 
Наряду со всеми этими возможностями в Kotlin также имеются корутины (coroutines, также их называют сопрограммами), которые упрощают работу.
Корутины (или легковесные потоки) не являются отдельными потоками, но несколько корутин могут совместно использовать один поток.
15. Проверяемые исключения, такие как IOException и FileNotFoundException, присутствуют в Java, но не поддерживаются в Kotlin. Причина в том, что они ничего не делают, кроме как содержат комментарий в блоке catch.

<a name="error-n+1"/>

## Ошибка N+1

Проблема N+1 это при fetch.Type.EAGER подгружается вся структура сущности + ее наследники (которых N штук). Каждая из дочерних сущностей подгружается отдельным запросом. Итого идут запросы на получение N (всех связанных элементов)+ 1(основной элемент).

Подход Spring Data:  
``@Fetch.Type.Lazy``

User one2many Role:  

```
public interface UserRepository extends CrudRepository<User, Long> {
// Проблема
    List<User> findAllBy(); // происходит проблема N+1

// Решение 1
    @Query("SELECT p FROM User p LEFT JOIN FETCH p.roles")  
    List<User> findWithoutNPlusOne(); // используя LEFT JOIN, мы решаем проблему N + 1

// Решение 2
    @EntityGraph(attributePaths = {"roles"})                
    List<User> findAll(); //используя attributePaths, Spring Data JPA позволяет избежать проблемы N + 1

}
```

<a name="serialization-deserialization"/>

## Сериализация и десериализация
Сериализация — это процесс сохранения состояния объекта в поток.  
Десериализация — это процесс восстановления объекта из потока.

Сериализовать можно только те объекты, которые реализуют интерфейс ``Serializable``. Этот интерфейс не определяет никаких методов, просто он служит указателем системе, что объект, реализующий его, может быть сериализован.

Для сериализации объектов в поток используется класс ``ObjectOutputStream``. Он записывает данные в поток.

Класс ``ObjectInputStream`` отвечает за обратный процесс - чтение ранее сериализованных данных из потока. В конструкторе он принимает ссылку на поток ввода.

По умолчанию сериализуются все переменные объекта. Однако, если мы хотим, чтобы некоторые поля были исключены из сериализации, они должны быть объявлены с модификатором transient.

<a name="multithreading"/>

## Многопоточность Java

Способы создания потока:

1. Создать объект класса Thread, передав ему в конструкторе нечто, реализующее интерфейс Runnable и вызвать start(). В классе, реализующем интерфейс переопределить единственный метод run(), внутри которого указать, что конкретно будет выполняться данным потоком.
2. Наследоваться от класса Thread и переопределить его метод run(). После этого создать объект собственного класса и вызвать start().

Эти способы не используются на реальных проектах. У разработчика не должно быть возможности самому создавать треды, иначе может начать вылетать ошибки. Например, Разработчик создал много тредов и, так как под каждый новый тред выделяется фиксированное количество мегабайт (например, 1Мб), то программа начинает уходить в своп при переполнении оперативной памяти. 
3. Использовать concurrent.ExecutorService - фреймворк для работы с потоками. Также в этом фреймворке есть классы для работы с ассинхронностью.

**Как сделать метод потокобезопасным?**
Прописать ``synchronized`` Можно сделать синхронизацию либо по объекту, либо по методу.

**Какие есть методы для работы с потоками?**
wait(), notify(), notifyAll()
Их можно использовать только в synchronized блоках.

**Какие ситуации могут возникнуть при работе с потоками?**
1. Deadlock, или взаимная блокировка, возникает, когда есть несколько потоков и каждый ожидает ресурс, принадлежащий другому потоку, так что формируется цикл из ресурсов и ожидающих их потоков. Наиболее очевидным видом ресурса является монитор объекта, но любой ресурс, который вызывает блокировку (например,wait/notify), также подходит.

Взаимная блокировка происходит, если в одно и то же время:
- Один поток пытается перенести данные с одного аккаунта на другой и уже наложил блокировку на первый аккаунт.
- Другой поток пытается перенести данные со второго аккаунта на первый, и уже наложил блокировку на второй аккаунт.

Предотвращение deadlock:
- Порядок блокировок — всегда накладывайте блокировки в одном и том же порядке.
- Блокировка с тайм-аутом — не блокируйте бессрочно при наложении блокировки, лучше как можно быстрее снимите все блокировки и попробуйте снова.

JVM способен обнаруживать взаимные блокировки мониторов и выводить информацию о них в дампах потоков.

2. Livelock и потоковое голодание. Livelock возникает, когда потоки тратят все свое время на переговоры о доступе к ресурсу или обнаруживают и избегают тупиковой ситуации так, что поток фактически не продвигается вперед. Голодание возникает, когда потоки сохраняют блокировку в течение длительных периодов, так что некоторые потоки «голодают» без прогресса.

3. RaceCondition. Состояние гонки возникает, когда один и тот же ресурс используется несколькими потоками одновременно, и в зависимости от порядка действий каждого потока может быть несколько возможных результатов. Код, приведенный ниже, не является потокобезопасным, и переменная value может быть инициализирована больше, чем один раз, так как check-then-act (проверка на null, а затем инициализация), которая лениво инициализирует поле, не является атомарной

```
class Lazy <T> {
 private volatile T value;
 T get() {
   if (value == null)
     value = initialize();
   return value;
 }
}
```

<a name="lambda-expressions"/>

## Лямбда-выражения

Лямбда-выражение — это такая функция. По сути, это анонимный (без имени) класс или метод, который можно передавать в другие методы в качестве аргумента.

Основу лямбда-выражения составляет лямбда-оператор, который представляет стрелку ->. Этот оператор разделяет лямбда-выражение на две части: левая часть содержит список параметров выражения, а правая собственно представляет тело лямбда-выражения, где выполняются все действия.

Лямбда-выражение не выполняется само по себе, а образует реализацию метода, определенного в функциональном интерфейсе. Функциональный интерфейс (@FunctionalInterface) - интерфейс с одним абстрактным методом. Например: consumer, supplier, function, predicate, operator и их биформы. Количество default методов не ограничено.

Лямбда строится так: (параметры) -> (код метода)

Пример:
```
public class LambdaApp {
 
    public static void main(String[] args) {
         
        Operationable operation;
        operation = (x,y)->x+y;
         
        int result = operation.calculate(10, 20);
        System.out.println(result); //30
    }   
}
interface Operationable{
    int calculate(int x, int y);
}
```

<a name="task-solutions"/>

## Решение заданий

## Задание 1
Необходимо в классе B на месте ? поставить все возможные варианты, чтобы все методы были корректно переопределены.
```
public static class A {

    public A methodA(A a) throws IOException {
        return null;
    }

    public A[] methodArrayA(A[] a) throws IOException {
        return null;
    }

    public List<A> methodArrayA(List<A> a) throws IOException {
        return null;
    }
}

public static class B extends A {

    @Override
    public ? methodA(? a) ? {
        return null;
    }

    @Override
    public ? methodArrayA(? a) ? {
        return null;
    }

    @Override
    public ? methodArrayA(? a) ? {
        return null;
    }
}
```
Решение:
```
public static class B extends A {

    @Override
    public A/B methodA(A a) throws IOException {
        return null;
    }

    @Override
    public A[]/B[] methodArrayA(A[] a) throws FileNotFoundException {
        return null;
    }

    @Override
    public List<A> methodArrayA(List<A> a) {
        return null;
    }
}
```
Сигнатура метода при его переопределении должна сохраняться. Для исключений разрешается сужение диапозона, а также полное отбрасывание конструкции throws. List является сложной структурой, поэтому его тип нельзя поменять на тип класса наследника.
## Задание 2
Необходимо вернуть map, которая подсчитывает количество повторений каждого элемента в list.
```
public static Map<Integer, Integer> countNumber(List<Integer> input) {
    return ?;
}

public static void main(String[] args) {
    final List<Integer> list = new ArrayList<>(List.of(1, 2, 4, 2, 1, 5, 8, 1));
    list.add(null);
    list.add(null);
    System.out.println(countNumber(list));
}
```
Решение:  
```
public static Map<Integer, Integer> countNumber(List<Integer> input) {
    return input.stream().distinct()
            .collect(Collectors.toMap(e -> e, e -> Collections.frequency(input, e)));
}

public static void main(String[] args) {
    final List<Integer> list = new ArrayList<>(List.of(1, 2, 4, 2, 1, 5, 8, 1));
    list.add(null);
    list.add(null);
    System.out.println(countNumber(list));
}
```
Map разрешает хранение null элементов, а также использование null в качестве ключа. Hashcode для null будет равен 0.
## Задание 3
Что будет в результате выполнения функции main и почему?
```
static class Person {

    private int num;
    private String name;

    public Person(int num, String name) {
        this.num = num;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if(this == o) return  true;
        if(!(o instanceof Person)) return false;
        Person person = (Person) o;
        return num == person.num && Objects.equals(name, person.name);
    }

    @Override
    public String toString() {
        return "Person{" +
                "num=" + num +
                ", name='" + name + '\'' +
                '}';
    }
}

public static void main(String[] args) {
    Set<Person> persons = new HashSet<>();

    persons.add(new Person(1, "Ivan"));
    persons.add(new Person(1, "Ivan"));
    persons.add(new Person(2, "Igor"));
    persons.add(new Person(3, "Vova"));

    System.out.println(persons.size());
}
```
Ответ:
Будут добавлены все 4 элемента, т.к. у всех объектов будут разные хэшкоды. При добавлении элементов в set происходит сначала их сравнение по хэшам и если они разные - элемент добавляется.  В классе Person нарушен контракт equasl и hashcode. Переопределяя equals - переопределяй и hashcode.
HashSet под капотом содержит Map. В Map массив односвязных списков - бакетов, размерностью 16. Когда количество непустых бакетов в map становится равным или больше n * k, где k - коэффициент, размер массива увеличивается в 2 раза и для каждого элемента вновь считается его ячейка для нового n.
## Задание 4
Необходимо вернуть массив уникальных чисел от 1 до size, значения в котором идут в случайном порядке.
```
public static void main(String[] args) {
    final int[] ints = mixInts(1000000);
}

private static int[] mixInts(int size) {
    
}
```
Решение:
```
private static final Random random = new Random();

public static void main(String[] args) {
    final int[] ints = mixInts(1000000);
}

private static int[] mixInts(int size) {
    List<Integer> numbers = new ArrayList<>(size);
    for (int i = 1; i <= size; i++) {
        numbers.add(i);
    }
    int[] mixInts = new int[size];
    for (int i = 0; i < size; i++) {
        mixInts[i] = numbers.remove(random.nextInt(numbers.size()));
    }
    return mixInts;
}
```
## Задание 5
Что будет выведено в результате выполнения метода main? Какой конструктор класса B будет вызван при передаче объекта класса C?
```
public class Task {
 
    public static class A {
        static {
            System.out.println("static A");
        }
 
        {
            System.out.println("block A");
        }
 
        public A() {
            System.out.println("construct A");
        }
    }
 
    public static class B extends A {
        static {
            System.out.println("static B");
        }
 
        {
            System.out.println("block B");
        }
 
        public B() {
            System.out.println("construct B");
        }
 
        public B(A a) {
            System.out.println("construct B(A)");
        }
 
        public B(B b) {
            System.out.println("construct B(B)");
        }
    }
 
    public static class C extends B {
        static {
            System.out.println("static C");
        }
 
        {
            System.out.println("block C");
        }
 
        public C() {
            System.out.println("construct C");
        }
    }
 
    public static void main(String[] args) {
        new B(new C());
    }
}
```
Ответ:
```
static A
static B
static C
block A
construct A
block B
construct B
block C
construct C
block A
construct A
block B
construct B(B)  
```
Пояснение:   
Инициализация происходит всегда от класса родителя к классам наследникам. Сначала будут выполнены статические блоки. Инициализация обычных блоков происходит перед конструктором.
