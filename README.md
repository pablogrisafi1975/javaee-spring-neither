# Java EE | Spring | Nothing

>Better than a comparison: A dictionary between worlds

## Table of Content


* Initial Notes
* Infrastructure-Servers
* Infrastructure-Change Servers
* Infrastructure-Change Implementation
* Infrastructure-Remove Framwework
* Core-Dependency Injection
* Core-Configuration
* Sql-Declarative Transactions
* Sql-jdbc
* Sql-ORM
* Sql-Higher Abstraction Level
* NoSql
* Web-Security
* Web-Component based MVC
* Web-Action based MVC
* Web-Reactive
* Web-WebSockets
* Web-ServerSentEvents
* Web-Rest
* Schedulled tasks
* Development-Startup
* Development-IDE
* Development-Debug
* Final Notes

## Initial Notes

 * In this doc, framework tipycally means either **Java EE**, **Spring** or **Nothing**. 
 * **Nothing** is for people who dislike both Spring and JEE 
 * Competence between frameworks is a good thing.
 * This is not the place to say framework A is better than framework B.
 * This is a place for the guy who normally works in framework A, and someday has to work in framework B, and wants to know at least how is some feature named in framework B, and some details about it.
 * Probably everything that can be done in framework A can be done in framework B, with some external library help or just writing more code
 * My original ordering idea was Java EE | Spring | Nothing, (Real standard, popular alternative, total freedom) but I ended up with Spring first because I'm more familiar with Spring (and I think it has more features, but that's just my opinion),
 * I'm focused in web apps because that's what I do for a living.
 * English is not my language, be gentle.
 * Don't link. Links are quickly outdated, and people can google what they need, if they have the right name.
 * Use the following format:
```md
### Category-Subcategory
Subcategory description
#### Spring
Feature name and brief description
#### Java EE
Equivalent feature or library, name and  brief description
#### Nothing
Equivalent feature or library, name and  brief description
#### Conclusion
Some final thoughts
```

## Dictionary


### Infrastructure-Servers
Which servers can I use to run my WebApp?
#### Spring
Pretty much any servlet or application container: Tomcat, Jetty, 
GlassFish, JBoss, Wildfly, WebSphere, Payara. The specific version of 
Spring you are using is tipically compatible with a range of versions of
the server. You can include the server in your app and deploy as a
complete jar, you can install in a running server just for your app or
even share the server with other apps. 
#### Java EE
Pretty much any application container: GlassFish, JBoss, Wildfly,
WebSphere, Payara. The specific version of JEE you are using is tipically
compatible with a range of versions of the server. You can include the
server in your app and deploy as a complete jar, you can install in a
running server just for your app or even share the server with other
apps. 
#### Nothing
Any server you like, everything already mentioned plus some really odd
things like nanohttpd or even the one already present in you JRE
(com.sun.net.httpserver.HttpServer).
#### Conclusion
You can use anything if you are not using Spring or JEE, Spring requieres
a servlet container, JEE an application container wich is a larger beast.
But don't let them fool you: while back in the day a full application
cotainer was a resource hungry, slow starter , memory eater 2 GB monster,
today there are excelent implementations like Wildfly or Payara Micro
that start as fast as Jetty and use about the same memory and disk space.

---
### Infrastructure-Change Server
Can I change the server I'm using?
#### Spring
Yes, very easily. Spring is a collection of jars you can install in any
compatible sever. It is couple of hours work.
#### Java EE
Yes, but maybe not so easily. While JEE is a standard, most
implementations give you some extra niceties you need to carefully avoid
if you want to keep your app compatible. And there are some
incompatibilities you will find even if you are carefull. But it *is*
doable, even if it is a couple of days work.
#### Nothing
Yes, but depending on the old vs new server features and details you will probably need to change some code.
#### Conclusion
You can always change it.

---
### Infrastructure-Change implementation
Can I change the implementation I'm using?
#### Spring
No. Spring is the only implementation of Spring, so no.
#### Java EE
Yes, it's the same as changing servers. (I'm not aware of any pluggable
Java EE implementation that can be deployed on different servers, or if that makes any sense)
#### Nothing
I don't know what are you talking about.
#### Conclusion
There is no direct comparation in this case.

---
### Infrastructure-Remove framework
Can I remove the framwork I'm using and use Nothing instead?
#### Spring
Yes, but you will need to implement a subset of Spring.
#### Java EE
Yes, but you will need to implement a subset of Java EE.
#### Nothing
You are already using Nothing.
#### Conclusion
There is no direct comparation in this case

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
#### Nothing
Google Guice, Dagger, PicoContainer can provide you with DI. Or you can
not use DI and handle your dependencies by yourself.
#### Conclusion
Don't let them fool you, neither in Spring nor in JEE you need to write a
single XML line if you don't want to. And both give you a pretty similar
set of features. 

---
### Core-Configuration
Reading configuration files, handling different values for dev/beta/prod environments.
#### Spring
Can read classical properties and yaml files, handling different environments via naming conventions (application-beta.properties) and supports placeholders like `app.description=${app.name} is my app`. Annotations can directly read the value of properties `@Value("${app.description}")`
#### Java EE
There is no special support for property files, but most implementations
provide some sort of support, from simply reading specific files to GUI
to edit them. Apache DeltaSpike provides several Spring like features
and more.
#### Nothing
Apache Commons Configuration and Typesafe Config give you lots of property
reading facilities. Google Guice has some embedded property support.
#### Conclusion
The lack of support in Java EE can be easily fixed, Spring however has more options out of the box.
___
___


#### Final notes
Made with love, [(GitHub-Flavored) Markdown Editor](https://jbt.github.io/markdown-editor/) and [Visual Studio Code](https://code.visualstudio.com/)

