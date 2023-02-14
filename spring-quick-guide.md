# Spring 是甚麼

> Spring Framework 是 Java 平台利用依賴注入（Dependency Injection, DI）與控制反轉（Inversion of Control, IoC）核心概念實現的 Web 應用程式開源框架，大幅簡化過去 Java EE Web 應用程式開發，為 Java EE 平台重新構建出許多 Web 應用支援，目前該框架許多核心功能也都可以用於大部份 Java 應用。
> Spring 使用POJO進行輕量級及最小侵入式開發，加上利用控制反轉（Inversion of Control, IoC）核心觀念貫穿，採取依賴注入（Dependency Injection, DI）與介面的方式達成元件鬆散耦合（loose coupling），而剖面導向程式設計（Aspect Oriented Programming, AOP）是將程式功能進行分離切分成不同的模組，各司其職。

# Spring Framework 有甚麼

![](./images/spring/01_SpringFrameworkArch.png)

- **Core** : 提供核心功能：DI，國際化，檢核與AOP
- **Data Access** : 藉由以下Java API做資料貯存 JTA (Java Transaction API), JPA (Java Persistence API), and JDBC (Java Database Connectivity)
- **Web** : 支援 Servlet API (Spring MVC) and of recently Reactive API (Spring WebFlux), 額外支援WebSockets, STOMP, 和WebClient
- **Integration** : 藉由以下Java規範來與其他JavaEE的系統整合 JMS (Java Message Service), JMX (Java Management Extension), and RMI (Remote Method Invocation)
- **Testing** : 提供測試方法(與Junit不同)


## 簡單來說甚麼是IOC(Inversion of Control)

讓我們來個簡單的範例，先定義一個`Company`類別：

```java
public class Company {
    private Address address;

    public Company(Address address) {
        this.address = address;
    }

    // getter, setter and other properties
}
```

`Company`會依賴`Address`這個類別

```java
public class Address {
    private String street;
    private int number;

    public Address(String street, int number) {
        this.street = street;
        this.number = number;
    }

    // getters and setters
}
```

- 傳統作法

如果要一個Company物件，我們會這樣寫：

```java
Address address = new Address("High Street", 1000);
Company company = new Company(address);
```

但如果我們有幾百個這樣的依賴關係，有時我們整個程式都使用這樣有依賴類別，有時候我們還要new一個新的，這樣的情況只會讓程式越來越亂，這時候IOC就來拯救世界了。把IOC想像成是一個容器(container)，裡面會有無數的物件，而IOC容器會管理他們之間的依賴關係。為了瞭解，直接上Code，不過我們不會自己去做一個IOC容器，我們會用`Spring`來實作

- 聲明那些物件要給`Spring`管理

首先是`Company`，這邊多加了`@Component`

```java
@Component
public class Company {
    // this body is the same as before
}
```

然後告訴`Spring`要`Company`與`Address`的依賴

```java
// 告訴Spring這是設定
@Configuration
// Spring不會知道有哪幾個是寫上@Component，要指定位置
@ComponentScan(basePackageClasses = Company.class)
public class Config {
    @Bean
    public Address getAddress() {
        return new Address("High Street", 1000);
    }
}
```

這個`@Configuration`會產生出新的物件，在`Spring`我們叫做`bean`。

- 該讓`Spring`出馬了

剛才提到的IOC容器，在`Spring`有個實現是`AnnotationConfigApplicationContext `

```java
ApplicationContext context = new AnnotationConfigApplicationContext(Config.class);
```

以下結果通會通過測試：

```java
Company company = context.getBean("company", Company.class);
assertEquals("High Street", company.getAddress().getStreet());
assertEquals(1000, company.getAddress().getNumber());
```

有興趣想跑可以參考這個範例，在`springbean`資料夾下：

https://github.com/eugenp/tutorials/tree/master/spring-core

## 如何叫Spring幫我們管Bean(Spring Bean Annotations)

通常我們會用Annotation`@`來標註(這個是Java功能)，以下幾個Annotations寫在類別上之後`Spring`將會自動接管。

- `@Component`
標註後Spring將會接管成Spring bean，無特別功能
- `@Repository`
實作自`@Component`，除了Spring bean的功能外，主要負責DB的資料層
- `@Service`
實作自`@Component`，給人類看的，無特別功能
- `@Controller`
這個Annotations是由`SpringMVC`提供，之後會多做解釋
- `@Configuration`
主要是做Bean的設定

## 再來說說DI(Dependency Injection)

其實你剛剛已經完成了依賴注入，看看我們的程式碼：

```java
// 告訴Spring這是設定
@Configuration
// Spring不會知道有哪幾個是寫上@Component，要指定位置
@ComponentScan(basePackageClasses = Company.class)
public class Config {
    @Bean
    public Address getAddress() {
        return new Address("High Street", 1000);
    }
}
```

你讓Spring幫你注入`Address`到`Company`，但想想：如果每次都這樣寫設定檔，不是很麻煩嗎？所以來介紹Spring其他相關的Annotations幫你自動注入。

- `@Autowired`