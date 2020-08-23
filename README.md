# formation-spring
Formation Excils Spring

# Spring
### Définition de Spring 

Spring est un Framework applicatif, il permet de faciliter le développement d’applications. Spring est né de l'idée de fournir une solution plus simple et plus légère que celle proposée par Java EE. C'est pour cette raison que Spring a été initialement désigné comme un conteneur léger.

L'idée principale de Spring est de proposer un framework qui utilise de simples POJO pour développer des applications plutôt que d'utiliser des EJB complexes dans un conteneur.

Il se repose sur 2 motifs de conception l’inversion de contrôle (IoC) et la programmation orientée aspect (AOP).

La première version de Spring date de 2003 à l'initiative de Pivotal Software. 
Aujourd’hui Spring est à la version 5. de la version 4 à la version 5, Spring a été réécrit en Java 8. Il n’est pas possible d’utiliser Spring 5 avec une version antérieur à Java 8.

On dit de Spring Framework qu'il est modulaire, puisqu'il propose des modules utilisables de façon indépendante et selon les besoins applicatifs. 

### Historique de Spring


### Alternative à Spring 

### Application de Spring 

### Fonctionnement de Spring 

### Modules de Spring 

#### Spring Core Container
 
* These modules provide IOC and Dependency Injection features.
* These modules provide IOC and Dependency Injection features.


#### Spring Web MVC 
Framework web de Spring, basé sur l'API servlet, permettant de mettre en place une application web suivant le pattern MVC.


#####DispatcherServlet

Servlet central de Spring MVC, permet le traitement des requêtes en déléguant le travail aux autres composants grâce à la config Spring.
Une application peut avoir plusieurs DispatcherServlet, chacun s'exécutant dans son propre namespace, avec son propre WebApplicationContext.
Seul l'ApplicationContext principal (celui chargé par le ContextLoaderListener) sera partagé.

![DispatcherServlet](annexes/pictures/mvc-context-hierarchy.png?raw=true "DispatcherServlet")

Voici un exemple Java d'initialisation d'un DispatcherServlet : 
```java
public class MyWebApplicationInitializer implements WebApplicationInitializer {

    @Override
    public void onStartup(ServletContext servletCxt) {

        // Load Spring web application configuration
        AnnotationConfigWebApplicationContext ac = new AnnotationConfigWebApplicationContext();
        ac.register(AppConfig.class);
        ac.refresh();

        // Create and register the DispatcherServlet
        DispatcherServlet servlet = new DispatcherServlet(ac);
        ServletRegistration.Dynamic registration = servletCxt.addServlet("app", servlet);
        registration.setLoadOnStartup(1);
        registration.addMapping("/app/*");
    }
}
```

Et voici un exemple XML :
```xml
<web-app>

    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/app-context.xml</param-value>
    </context-param>

    <servlet>
        <servlet-name>app</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value></param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>app</servlet-name>
        <url-pattern>/app/*</url-pattern>
    </servlet-mapping>

</web-app>
```

##### Beans utilisés par le DispatcherServlet
RequestMappingHandlerAdapter
Le DispatcherServlet délègue le travail au types de bean suivant : 
![DispatcherBeans](annexes/pictures/dispatcher-beans.png?raw=true "DispatcherBeans")

Les types par défaut utilisés si les beans requis ne se trouvent pas dans le WebApplicationContext se trouvent dans org.springframework.web.servlet.DispatcherServlet.properties:
```properties
org.springframework.web.servlet.HandlerMapping=org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping,\
	org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping,\
	org.springframework.web.servlet.function.support.RouterFunctionMapping

org.springframework.web.servlet.HandlerAdapter=org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter,\
	org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter,\
	org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter,\
	org.springframework.web.servlet.function.support.HandlerFunctionAdapter

org.springframework.web.servlet.HandlerExceptionResolver=org.springframework.web.servlet.mvc.method.annotation.ExceptionHandlerExceptionResolver,\
	org.springframework.web.servlet.mvc.annotation.ResponseStatusExceptionResolver,\
	org.springframework.web.servlet.mvc.support.DefaultHandlerExceptionResolver

org.springframework.web.servlet.ViewResolver=org.springframework.web.servlet.view.InternalResourceViewResolver

org.springframework.web.servlet.LocaleResolver=org.springframework.web.servlet.i18n.AcceptHeaderLocaleResolver

org.springframework.web.servlet.ThemeResolver=org.springframework.web.servlet.theme.FixedThemeResolver

org.springframework.web.servlet.FlashMapManager=org.springframework.web.servlet.support.SessionFlashMapManager
```

#### Traitement des requêtes
![RequestProcessing](annexes/pictures/request-processing.png?raw=true "DispatcherBeans")

#### Les vues
La technologie de vues dans Spring MVC est configurable. Celà peut être du Thymeleaf, Groovy, JSPs...

/!\ Les vues d'une application Spring MVC ont accès à tous les beans de l'application context.


#### Spring security 

#### Spring REST

### API RESTFUL 

# SpringBoot 

# Outil de stockage

# Ressources 
### Spring 
Spring Initialize : https://start.spring.io 

### Spring ORM 
Hibernate : https://hibernate.org 
### Git
Gitignore : https://www.toptal.com/developers/gitignore 

Git: https://git-scm.com/docs/git 

### Migration de base de données 
Flyway DB : https://flywaydb.org

Liquibase: https://www.liquibase.org  

### Loggers
SL4J : http://www.slf4j.org/manual.html 

### Tutoriels
Tutoriels Baeldung Spring :  https://www.baeldung.com/spring-tutorial

Tutoriels Baeldung Springboot : https://www.baeldung.com/spring-boot 
