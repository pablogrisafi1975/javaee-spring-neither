# Java EE | Spring | Neither

>Better than a comparison: A dictionary between worlds

## Table of Content


* [Initial Notes](#initial-notes)
* [Infrastructure-Servers](#infrastructure-servers)
* [Infrastructure-Change Server](#infrastructure-change-server)
* [Infrastructure-Change Implementation](#infrastructure-change-implementation)
* [Infrastructure-Remove Framework](#infrastructure-remove-framework)
* [Core-Dependency Injection](#core-dependency-injection)
* [Core-Configuration](#core-configuration)
* [Sql-Declarative Transactions](#sql-declarative-transactions)
* [Sql-JDBC](#sql-jdbc)
* [Sql-ORM](#sql-orm)
* [Sql-Higher Abstraction Level](#sql-higher-abstraction-level)
* [NoSql](#nosql)
* [Web-Component based MVC](#web-component-based-mvc)
* [Web-Action based MVC](#web-action-based-mvc)
* [Web-Reactive](#web-reactive)
* [Web-Rest](#web-rest)
* [Web-Security](#web-security)
* [Scheduled tasks](#scheduled-tasks)
* [Development-Startup](#development-startup)
* [Development-IDE](#development-ide)
* [Final Notes](#final-notes)

## Initial Notes

 * In this doc, framework means either **Java EE** or **Spring**.
 * **Neither** is for people who dislike both Spring and JEE 
 * Competence between frameworks is a good thing
 * This is not the place to say framework A is better than framework B
 * This is a place for the guy who normally works in framework A, and
 someday has to work in framework B, and wants to know at least how is
 some feature named in framework B, and some details about it
 * Probably everything that can be done in framework A can be done in
 framework B, with some external library help or just writing more code
 * My original ordering idea was Java EE | Spring | Neither, (Real
 standard, popular alternative, total freedom) but I ended up with Spring
 first because I'm more familiar with Spring (and I think it has more
 features, but that's just my opinion)
 * I'm focused in web applications because that's what I do for a living
 * English is not my language, be gentle.
 * Write a final dot in every sentence. 
 * Don't link. Links are quickly outdated, and people can search what
 they need, if they have the right name.
 * Use the following format:
```md
### Category-Subcategory
Subcategory description
#### Spring
Feature name and brief description
#### Java EE
Equivalent feature or library, name and  brief description
#### Neither
Equivalent feature or library, name and  brief description
#### Conclusion
Some final thoughts

---
```

## Dictionary


### Infrastructure-Servers
Which servers can I use to run my WebApp?
#### Spring
Pretty much any servlet or application container: Tomcat, TomEE, Jetty, 
GlassFish, JBoss, Wildfly, WebSphere, Payara. The specific version of 
Spring you are using is compatible with a range of versions in
the server. You can include the server in your app and deploy as a
complete jar, you can install in a running server just for your app or
even share the server with other apps.
#### Java EE
Pretty much any application container: GlassFish, JBoss, Wildfly, TomEE
WebSphere, Payara. The specific implementation of JEE you are using
includes the server. You can deploy to a working server, or include the
server in your app and deploy as a complete jar, or even share the server
with other Java EE applications.
#### Neither
Any server you like, everything already mentioned plus some really odd
things like nanohttpd or even the one already present in you JRE
(com.sun.net.httpserver.HttpServer).
#### Conclusion
You can use anything if you are not using Spring or JEE, Spring requieres
a servlet container, JEE an application container wich is a larger beast.
But don't let them fool you: Back in the day an application container was
a resource hungry, slow starter , memory eater 2 GB monster, today there
are excelent implementations like Wildfly or Payara Micro that start as
fast as Jetty and use about the same memory and disk space.

---

### Infrastructure-Change Server
Can I change the server I'm using?
#### Spring
Yes, very easily. Spring is a collection of jars you can install in any
compatible sever. It is couple of hours work.
#### Java EE
Yes, but maybe not so easily. While JEE is a standard, most
implementations give you some extra niceties you need to carefully avoid
if you want to keep your application compatible. And there are some
incompatibilities you will find even if you are carefull. But it *is*
doable, even if it is a couple of days work.
#### Neither
Yes, but depending on the old vs new server features and details you will 
probably need to change some code.
#### Conclusion
You can always change it.

---

### Infrastructure-Change implementation
Can I change the implementation I'm using?
#### Spring
No. Spring is the only implementation of Spring, so no.
#### Java EE
Yes, it's the same as changing servers. (I'm not aware of any pluggable
Java EE implementation that can be deployed on different servers, or if
that makes any sense). However, Java EE is a collection of several
components and some of them are more likely to be changed: TomEE ships
with OpenJPA for persistence, you can switch to Hibernate easily. Most
implementations of the Java EE standard allow to easy change the JSF
implementation.
#### Neither
I don't know what are you talking about.
#### Conclusion
Java EE is more flexible in this case.

---

### Infrastructure-Remove framework
Can I remove the framework I'm using and use Neither instead?
#### Spring
Yes, but you will need to implement a subset of Spring.
#### Java EE
Yes, but you will need to implement a subset of Java EE.
#### Neither
You are already using Neither.
#### Conclusion
Depending how much you are using Spring or Java EE, it can be easy, hard,
impossible.

---

### Core-Dependency Injection
You probably know what I'm talking about.
#### Spring
Spring is basically a DI framework plus other things. You can declare
your dependencies in XML, java or groovy files, or use automatic
injection. You can combine all those methods in one app. You can inject
dependencies, resources, configuration file values and even command line
arguments.
#### Java EE
CDI (context and dependency injection) is the JEE equivalent. It can use
XML or annotations. The context injection (the C in CDI) is a powerful
concept I don't think Spring offers.
#### Neither
Google Guice, Dagger, PicoContainer can provide you with DI. Or you can
not use DI and handle your dependencies by yourself.
#### Conclusion
Don't let them fool you, neither in Spring nor in Java EE you need to
write a single XML line if you don't want to. And both give you a pretty
similar set of features. 

---

### Core-Configuration
Reading configuration files, handling different values for dev/beta/prod
environments.
#### Spring
Can read classical properties and yaml files, handling different
environments via naming conventions (application-beta.properties) and
supports placeholders like `app.description=${app.name} is my app`.
Annotations can directly read the value of properties `@Value("${app.description}")`
#### Java EE
There is no special support for property files, but most implementations
provide some sort of support, from simply reading specific files to GUI
to edit them. Apache DeltaSpike provides several Spring like features
and more.
#### Neither
Apache Commons Configuration and Typesafe Config give you lots of property
reading facilities. Google Guice has some embedded property support.
#### Conclusion
The lack of support in Java EE can be easily fixed, Spring however has
more options out of the box.

---

### Sql-Declarative Transactions
Handle transaction commit/rollback via annotations or configuration files.
#### Spring
The `@Transactional` annotation, typically used at service level, affects
every transactional resource involved that Spring is aware of. Spring
however **can not** natively span a transaction over several databases.
If  need to commit to more than one DB you need to use an external
transaction manager, like Atomikos or Bitronix, wich are easily
integrated into Spring.
#### Java EE
The `@Transactional` annotation, typically used at service level, affects
every transactional resource involved that Java EE is aware of. Java EE
**can** span a transaction over several databases. 
#### Neither
Guice has some support for `@Transactional` on JPA database access. 
Atomikos can be integrated to any system.
#### Conclusion
While Spring transaction management is somehow more flexible, it lacks 
the power to handle transactions that affect more than one database.
That can easily fixed integrating Atomikos or Bitronix.

---

### Sql-JDBC
Direct access and support for JDBC connections without much boilerplate.
#### Spring
Spring JDB templates can take care of opening and closing the connection,
statement and resultset as needed. It can an usually automatically map
columns to fields with basic naming handling (FIRST_NAME maps to
firstName) and allows RowMappers to flexible map query results to DTOs.
You can have named parameters and also help with basic insert/updates.
#### Java EE
Nothing by default, try Apache Commons DbUtils or JDBI.
#### Neither
Apache Commons DbUtils and the more modern JDBI can give you everything
you need to handle JDBC connections without boilerplate 
#### Conclusion
Java EE is not very JDBC friendly, you are expected to use JPA. You can 
integrate Apache Commons DbUtils or JDBI to simplify JDBC access. 

---

### Sql-ORM
Work like domain objects, persist like rows.
#### Spring
Spring integrates well with Hibernate, Java Persistence API (JPA), Java
Data Objects (JDO), MyBatis.
#### Java EE
JPA and JDO are basic building blocks in Java EE. Hibernate is a JPA
provider (so you can use it as any other JPA compatible provider) and you
can easily access directly the Hibernate API if you want to.
#### Neither
Hibernate can be used without any framework if you want. There are other
more lightweight alternatives like ebean-orm or OrmLite.
#### Conclusion
Everyone can use Hibernate without much hassle. Java EE and Spring have
JPA support. Spring has a couple of extra alternatives, not so popular.
There are lightweight alternatives if you use Neither.

---

### Sql-Higher Abstraction Level
Automatic repository/DAO creation.
#### Spring
Spring Data can generate runtime implementation of methods based on
names. You write something like
```
  interface PersonRepository extends Repository<Person, Long> {
    List<Person> findByLastname(String lastname);
  }
```   
And the implementation is automatically generated. Works with JPA,
MongoDB, Cassandra and other forms of data storage.
#### Java EE
There is no direct support, but Apache Delta Spike provides similar
features (although only for JPA)
#### Neither
I'm not aware of any stand alone project like this.
#### Conclusion
Spring has the most powerful version, Java EE is still behind on this.
Couldn't find anything that works without Spring of Java EE.

---

### NoSql
Non RDBM ways to store/retrieve/query data.
#### Spring
Spring Data gives you automatic repositories over Mongo, Cassandra, Redis
and some other engines. While the basics remains similar, some things may
not be possible (or ma be too expensive) in a  determinated engine. 
#### Java EE
There is no direct support.
#### Neither
I'm not aware of any stand alone project like this.
#### Conclusion
AFAIK, Spring has the clear advantage here.
Couldn't find anything similar that works without Spring.

---

### Web-Component based MVC
Web framework based in components (JSF style).
#### Spring
No out of the box support. JoinFaces project enables JSF usage inside Spring.
#### Java EE
JSF is the basic way to make web applications in Java EE. There are several
libraries of components ( PrimeFaces, PrimeFaces Extensions, BootsFaces, 
ButterFaces, RichFaces, OmniFaces, AngularFaces, Mojarra, MyFaces) and most
of them can be used in any implementation. 
#### Neither
I'm not aware of any jsf-like library that you can use without an application
server, or Spring pretending to be one. 
#### Conclusion
This was one of main selling points of Java EE and one of the most loved and
hated features. Client side web development seems to be moving now to
Javascript frameworks like Angular or React, and web servers just expose services.

---

### Web-Action based MVC
Web framework based in actions (Classic MVC/Struts style)
#### Spring
Spring MVC can map forms to POJO's, handles validations, file upload/download,
path/query/header/cookies parameters, template engines like JSP, Velocity and 
Freemarker, support Websockets and ServerSentEvents.
#### Java EE
There was a MVC 1.0 project that was supposed to bring action based MVC to JEE 
but was abandoned.
#### Neither
There are tons of frameworks that provide the same functionality: Apache Struts, 
Tapestry, Wicket, Stripes, Grails.
#### Conclusion
JEE does not have support for this, but again, client side web development seems 
to be moving now to Javascript frameworks like Angular or React, and web servers 
just expose rest services.

---

### Web-Reactive
Reactive Web framework
#### Spring
Spring 5.0 has a new web framework, webflux, that supports reactive programming
through an extension of RxJava called Reactor. It is suppossed to have the same
functionality as the classic Spring MVC but in an asynchronious reactive way.
#### Java EE
I'm not aware of anything.
#### Neither
There are some of frameworks that provide the same functionality: Akka, Vert.x, 
RxJava, Reactor.
#### Conclusion
JEE does not have support for this new paradigm, but as always, you can integrate
some standalone alternatives.

---

### Web-Rest
Rest Web framework.
#### Spring
Spring has no framework/library/component specifically designed to Rest. However
you can get most functionallity required through MVC, Spring Data repository and
Spring HATEOAS.
#### Java EE
JAX-RS is the specification, and Jersey is the reference implementation. It is 
very popular and has erything you may need aout of the box.
#### Neither
Jersey itself can be used without JEE. There are several frameworks that provide 
the same functionality: SparkJava, Dropwizard, RestEasy, Rapidoid.
#### Conclusion
You can do rest services pretty much with everything.

---

### Web-Security
Security (Authentication and Authorization) for your application.
#### Spring
Spring Security offers authentication and authorization, plus protection against 
attacks like session fixation, clickjacking, cross site request forgery, etc.
You have users with roles, and annotations in your public methods with grant/revoke
access to them, like `@PreAuthorize("hasRole('USER')")`.
#### Java EE
Java Authentication and Authorization Service (JAAS) offers authentication and
authorization. You have users with roles, and annotations in your public methods 
with grant/revoke access to them, like `@RolesAllowed("USER")`.
#### Neither
Apache Shiro, Pac4j and others can give you authentication and authorization.
#### Conclusion
Spring is a little more powerful in declarative configuration, since you can
have expression in the configuration. Anyway, every framework supports programmatic
configuration, so you can be as flexible and precise as you want in java.

---

### Scheduled tasks
Potentially long tasks that run at specific moments.
#### Spring
Spring Batch offers transaction management, chunk based processing, declarative I/O,
start/stop/restart/retry/skip tasks and a web based administration interface.
#### Java EE
JSR-352 is the specification of batch jobs for Java EE. It was heavily based in Spring
Batch, which in turn implements the specification. 
#### Neither
JBeret is the Wildfly implementation of JSR-352 and can be used standalone with some 
effort. For minimal requirements like run something at specific time, Quartz may be 
enough.
#### Conclusion
The programming models in JSR-352 and Spring Batch are pretty much the same. It is
more complicated, but possible, if you use Neither.

---

### Development-Startup
Tools that help you start a project from zero.
#### Spring
Spring Initializr helps you create the maven or graddle file and the folder structure
you need, with all the dependencies you choose. It is a great way to boostrap a web
application. Unfortunately it has no support for UI. JHipster (not from Spring) does
pretty much the same and also includes the basic support for an Angular UI, a CRUD
for every entity, administrator pages, metrics UI, and more.
#### Java EE
Haven't find anything like that. 
#### Neither
I don't thing there is a possible answer here. If you want Neither, you are probable 
not going to like to have a tool creating the basics of the project for you.
#### Conclusion
Spring is leading here. However, it is to be noted than staring the development in a 
Java EE environment is generally simpler, because lots of things are already present
in the server.

---

### Development-IDE
IDE plugins to help development within a specific framework
#### Spring
Eclipse: Spring Tool Suite can be used as an Eclipse distribuiton, or installed as
a plugin inside a working Eclipse. Offers autocomplete everywhere (config/xml/property
files) graphical tools and several more options.

IntelliJ: Has Spring support on Ultimate edition only.

Netbeans: has some support for Spring out of the box.

#### Java EE
Eclipse: there is a Eclipse IDE for Java EE Developers, and also some implementations
have their own set of plugins, like JBoss tools for Wildfly

IntelliJ: Has Spring support on Ultimate edition only.

Netbeans: has great support for Spring out of the box.

#### Neither
There is no possible answer.
#### Conclusion
While you don't need anything to use any framework, a specific tool can help you.
Netbeans and IntelliJ Ultimate have out of the box support, Eclipse requieres plugins.

---
___


### Final notes
Made with love, 
 [(GitHub-Flavored) Markdown Editor](https://jbt.github.io/markdown-editor/) and 
 [Visual Studio Code](https://code.visualstudio.com/)


