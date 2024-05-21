
Spring Boot is an open-source Java framework used to create  Micro Services.

## Tomcat

![[Screenshot 2024-04-18 at 9.26.12 AM (2).png]]

there are other web servers also for e.g jetty

set web server in application.yml
```yml
server:  
port: 8080  
  
spring:  
main:  
web-application-type: servlet
```

@SpringBootApplication
Wrapper for encapsulating @Configuration, @EnableAutoConfiguration and @ComponentScan annotations combine.

@Configuration
Configuration classes are user to create beans, conventionally called AppConfig, If you want to have a bean dependent on another bean you must define it inside of a config class.

@EnableAutoConfiguration
It makes Spring guess the config based on JAR files available on the classpath.

@ComponentScan
It is responsible for telling Spring where to look for Components.
By default, Spring will search within the package that the main class is located along with all of its child packages.

## Spring Web MVC

The Spring Web MVC(model-view-controller) framework provides a very easy way of implementing MVC architecture in our web applications.


@Controller
marks the class as web controller. A specialisation of @component annotation, which allows Spring to auto-detect implementation classes/beans by scanning classpath.


@RestController 
It is a convenience syntax for @Controller and @ResponseBody. 

@ResponseBody 
It is a utility annotation that tells Spring to automatically serialize return value(s) of this classes method into HTTP response.


## Jackson 

the Java JSON library
We don't need any logic to transfer our Java Objects to JSON.


## HTTP 

HTTP is a protocol for fetching resources such as HTML documents. It is a foundation of any data exchange on the Web and it is a client-service protocol, which means requests are initiated by the recipient, usually the Web browser.

HTTP Message  from http 1.0 onwards

1. Http Request Message - Mainly of type GET, POST, PUT, DELETE request.
2. Http Response Message - Contains http status code, data, content-type etc.
 

URL = Uniform Resource Locator

https://abc.com/courses/spring-boot

https:// - protocol

URN - Uniform Resource Name
abc.com - Host
:443 - port (usually hidden)
/courses/spring-boot - Resource path
/course?price=free - Query Parameters


@Service - alias for @Component we use this to be more specific
to instantiate class for usage

Where are these controller, dao, service classes are stored ?

They are store in ApplicationContext.

## Application Context

It provides basic functionalities for managing beans.
![[Screenshot 2024-04-18 at 3.38.32 PM.png]]

Application Context Extends BeanFactory represents Spring IOC  (Inversion of Control) which in spring world implemented by dependency injection.


```java
public static void main(String[] args) {  
  
ConfigurableApplicationContext applicationContext = SpringApplication.run(SpringBootProjectApplication.class, args);  
String[] beanDefinitionNames = applicationContext.getBeanDefinitionNames();  
for (String beanDefinitionName : beanDefinitionNames) {  
System.out.println(beanDefinitionName);  
}  
}
```


Bean Scopes - basically the visibility and life cycle of the bean throughout the application lifecycle.
![[Screenshot 2024-04-18 at 3.47.54 PM.png]]

# What is a Bean? 

Bean is an object that the spring container instantiates assemble and manages the entire lifecycle for us.

@Bean to make thing managed by application context

```java
@Bean  
public Foo getFoo() {  
return new Foo("bar");  
}  
record Foo(String name) {}
```


```java
@Bean  
CommandLineRunner commandLineRunner(CustomerRepository repository) {  
return args -> {  
// run some code on startup can inject dependencies by passing as parameters  
};  
}
```


## Hibernate 
ORM - Object Relational Mapping

Allows you to map objects to relational databases.

## JDBC

![[Screenshot 2024-04-19 at 12.15.01 PM.png]]


How to write DDL when we turn off hibernate ddl-auto?
We can use db migrations like flyway, liquibase etc

## Flyway 

Database versioning framework.


```xml
<dependency>  
<groupId>org.flywaydb</groupId>  
<artifactId>flyway-core</artifactId>  
</dependency>
```


db.migration inside resources

Naming
V2__Add_new_table.sql




BIGSERIAL - data type BIGINT but also add sequence to it

select nextval('customer_id_seq');  // to move nextval
select currval('cutomer_id_seq'); // to see curr val

never increment seq manually 

to set to default

SELECT setval('customer_id_seq', 1, false);

# [[Spring Boot Testing]]
## Spring Security

To secure your request with multiple security filters.

JWT Token 
jwt.io
copy dependencies from libraries to use them in your project

