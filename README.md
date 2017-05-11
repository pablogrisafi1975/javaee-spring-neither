# Java EE | Spring | Nothing

Better than a comparison: A dictionary between worlds

 * This is not the place to say A is better than B
 * This is a place for the guy who normally works in A, and someday has to work in B, and wants to know at least how is some feature named in B
 * Competence between options is a good thing
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
Pretty much any application container: GlassFish, JBoss, WebSphere, Payara. The specific version of JEE you are using is tipically compatible with a range of versions of the server. You can include the server in your app and deploy as a complete jar, you can install in a running server just for your app or even share the server with other apps. 
#### Nothing
Any server you like, everything already mentioned plus some really odd things like nanohttpd or even the one already present in you JRE (com.sun.net.httpserver.HttpServer)
#### Conclusion
You can use anything if you are not using Spring or JEE, Spring requieres a servlet container, JEE an application cotainer wich is a larger beast. But don't let them full you: while back in tha day a full application cotainer was a resource hungry, slow starter , memory eater 2 GB monster, today there are excelent implementations like Wildfly or Payara Micro start as fast as Jetty and use about the same memory and disk space

---
