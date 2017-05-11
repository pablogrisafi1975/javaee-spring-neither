# Java EE | Spring | Nothing

Better than a comparison: A dictionary between worlds

 * This is not the place to say A is better than B
 * This is a place for the guy who normally works in A, and someday has to work in B, and wants to know at least how is some feature named in B
 * Competence between options is a good thing
 * **Nothing** is for people who dislike both Spring and JEE 
 * Probably everything that can be done in A can be don in B, with some external library help or just writing more code
 * My idea was going from Java EE to Spring to Nothing, but I ended up with Spring first beacuse I'm more familiar with Spring (and I think it has more features, but that's just my opinion)
 * I'm focused in web apps because that's waht I do for a living
 * Don't link. Links are quickly outdated, and people can google what they need
 * Follow the format
---
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

---

## Now, let's go


### Infrastructure-Servers
Which servers can I use to run my WebApp ?
#### Spring
Pretty much any servlet or application container: Tomcat, Jetty, GlassFish, JBoss, Wildfly, WebSphere, Payara. The specific version of Spring you are using is tipically compatible with a range of versions of the server. You can include the server in your app and deploy as a complete jar, you can install in a running server just for your app or even share the server with other apps. 
#### Java EE
Pretty much any application container: GlassFish, JBoss, Wildfly, WebSphere, Payara. The specific version of JEE you are using is tipically compatible with a range of versions of the server. You can include the server in your app and deploy as a complete jar, you can install in a running server just for your app or even share the server with other apps. 
#### Nothing
Any server you like, everything already mentioned plus some really odd things like nanohttpd or even the one already present in you JRE (com.sun.net.httpserver.HttpServer)
#### Conclusion
You can use anything if you are not using Spring or JEE, Spring requieres a servlet container, JEE an application cotainer wich is a larger beast. But don't let them fool you: while back in the day a full application cotainer was a resource hungry, slow starter , memory eater 2 GB monster, today there are excelent implementations like Wildfly or Payara Micro that start as fast as Jetty and use about the same memory and disk space

---
### Infrastructure-Change Server
¿Can I change the server I'm using?
#### Spring
Yes, very easily. Spring is a collection of jars you can install in any compatible sever. It is couple of hours work 
#### Java EE
Yes, but maybe not so easily. While JEE is a standard, most implementations give you some extra niceties you need to carefully avoid if you want to keep your app compatible. And there are some incompatibilities you will find even if you are carefull. But it is doable, even if it is a couple of days work
#### Nothing
Yes, but depending on the old vs new server features and details you probably may need to change some code
#### Conclusion
You can always change it

---
### Infrastructure-Change implementation
¿Can I change the implementation I'm using?
#### Spring
Spring is the only implementation of Spring, so no
#### Java EE
Yes, it is tha same of changing server. I'm not aware of any pluggable implementation that can be deployed on different servers, or if that makes any sense 
#### Nothing
I don't know what are you talking about
#### Conclusion
There is no direct comparation in this case

---
### Infrastructure-Remove framework
¿Can I remove the framwork I'm using and use nothing instead?
#### Spring
Yes, but you will need to implement a subset of Spring
#### Java EE
Yes, but you will need to implement a subset of Java EE
#### Nothing
You are already using Nothing
#### Conclusion
There is no direct comparation in this case
