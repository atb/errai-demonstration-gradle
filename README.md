# Errai Demonstration

This is a demo application that demonstrates several Errai technologies.

Errai is a GWT-based framework for building rich web applications using next-generation web technologies. See [Errai](http://erraiframework.org).

GWT is a development toolkit for building and optimizing complex browser-based applications. With GWT, client and server parts of a web application are written in Java. 
See [GWT Project](http://www.gwtproject.org). 

This demonstration is based on [errai-jpa-demo-todo-list](https://github.com/errai/errai/tree/master/errai-demos/errai-jpa-demo-todo-list) 
but it has been updated to a "contact list application" and simplified as much as possible. 

## Prerequisites

 * Java JDK 8
    * You must download and properly install JDK 8 in your system   
 * Gradle
    * Gradle is downloaded when you use **gradlew**
 * WildFly 15.0.1.Final 
    * Wildfly is downloaded using the task **provision**

If you wish to configure a datasource in WidlFly, edit the file `standalone/configuration/standalone.xml`
and add this immediately after the similar entry for `ExampleDS`:

    <datasource jndi-name="java:jboss/datasources/ExampleDS" pool-name="ExampleDS" enabled="true" use-java-context="true">
        <connection-url>jdbc:h2:mem:test;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE</connection-url>
        <driver>h2</driver>
        <security>
            <user-name>sa</user-name>
            <password>sa</password>
        </security>
    </datasource>

Of course, you are encouraged to configure the data source to connect to a more permanent database
such as PostgreSQL or MySQL instead of H2. With the above "in-memory" configuration, the data you
enter into the demo will not survive restarts of the app server.

## Clean

    ./gradlew clean


## Download Wildfly

The following command will download wildfly and install it into the **wildfly** folder. 

    ./gradlew provision

## Build

The following command will compile the application and build a war file in **build/libs**.

    ./gradlew build    

## Start Wildfly

Use the following command to start Wildfly and the application

    ./gradlew startWildfly

After that you can access the application by using the following url: [http://localhost:8080/errai-demonstration-gradle/](http://localhost:8080/errai-demonstration-gradle/)

## Stop Wildfly

To stop Wildfly execute the following command

    ./gradlew stopWildfly

## Development

Any code changes can be redeployed without restarting the application server (i.e., 
Wildfly).

Start coding and redeploy with:

    ./gradlew redeploy

Compilation is separated in front-end (client) and back-end (server).
To avoid long recompilation, only the parts that changed will be recompiled.

## Super dev mode (debug client code)

When working on the front-end code (e.g., to debug client code), it is possible to enable super dev mode of GWT for quick front-end redeployment.
Run the following blocking command:

    ./gradlew gwtDev

Redeployment happens automatically on browser page refresh.

**Note:** You need to have Wildfly runnning!

Debug Server Code
-----------------

If you wish to debug the server code you need to open the project in a Java IDE. It 
is recommended to use Eclipse or IntelliJ.

You should set the breakpoints in the source code of the server part of the applications.

Start the wildly server with the following command:

    ./gradlew startWildflyDebug

Gradle will start Wildfly in debug mode and will wait until the IDE is connected to the debug 
session. In Eclipse you can do this by creating a "Remote Java Application" debug configuration setting host 
to localhost and port to 8787.

