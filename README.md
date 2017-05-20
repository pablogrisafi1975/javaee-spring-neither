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
* NoSql
* Web-Security
* Web-Component based MVC
* Web-Action based MVC
* Web-Reactive
* Web-WebSockets
* Web-ServerSentEvents
* Web-Rest
* Scheduled tasks
* Development-Startup
* Development-IDE
* Development-Debug
* Final Notes

## Initial Notes

 * In this doc, framework means either **Java EE** or **Spring** 
 * **Neither** is for people who dislike both Spring and JEE 
 * Competence between frameworks is a good thing.
 * This is not the place to say framework A is better than framework B.
 * This is a place for the guy who normally works in framework A, and
 someday has to work in framework B, and wants to know at least how is
 some feature named in framework B, and some details about it.
 * Probably everything that can be done in framework A can be done in
 framework B, with some external library help or just writing more code
 * My original ordering idea was Java EE | Spring | Neither, (Real
 standard, popular alternative, total freedom) but I ended up with Spring
 first because I'm more familiar with Spring (and I think it has more
 features, but that's just my opinion)
 * I'm focused in web applications because that's what I do for a living
 * English is not my language, be gentle
 * Don't link. Links are quickly outdated, and people can search what
 they need, if they have the right name
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
Nothing by default, try Apache Commons DbUtils or JDBI
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
more lightweight alternatives like ebean-orm or OrmLite 
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

___
___


### Final notes
Made with love, 
 [(GitHub-Flavored) Markdown Editor](https://jbt.github.io/markdown-editor/) and 
 [Visual Studio Code](https://code.visualstudio.com/)


