# Overview

This is a sample webapp that demonstrates batch job scheduling using Java EE Concurrency Utils.
The WAR package includes [jberet-schedule-executor module](https://github.com/jberet/jsr352/tree/master/jberet-schedule/jberet-schedule-executor)

This app also demonstrates how to configure the `JobScheduler` through `context-param` in 
[web.xml](https://github.com/jberet/jsr352/blob/master/wildfly-jberet-samples/scheduleExecutor/src/main/webapp/WEB-INF/web.xml) 
and a [ServletContextListener class](https://github.com/jberet/jsr352/blob/master/wildfly-jberet-samples/scheduleExecutor/src/main/java/org/jberet/samples/wildfly/schedule/executor/ContextListener1.java)

ScheduledExecutorService-based `JobScheduler` can be configured with:

 * a custom `ManagedScheduledExecutorService` JNDI lookup name (Java EE app only);
 * a `java.util.concurrent.ConcurrentMap<String, JobSchedule>` to store all job schedules;
 * fully-qualified name of the implementation class of `JobSchedue`.

## How to Build

    mvn clean install

## How to Run Tests

1. Start JBoss EAP 7 or WildFly server:
    
    ```
    $JBOSS_HOME/bin/standalone.sh
    ```
  
2. Run [tests](https://github.com/jberet/jsr352/blob/master/wildfly-jberet-samples/scheduleExecutor/src/test/java/org/jberet/samples/wildfly/schedule/executor/ScheduleExecutorIT.java)
    with `wildfly` profile:
    
    ```
    mvn -Pwildfly install
    ```
     
3. Undeploy application:
    
    ```
    mvn wildfly:undeploy
    ```
    
## How to Run with `jberet-ui`

 First, you will need to build `jberet-ui` module with `--restUrl` for this application deployment:
 
 ```
 cd <project-home>/jberet-ui
 gulp --restUrl http://localhost:8080/scheduleExecutor/api/
 ```
 
 To incluee `jberet-ui` module into the WAR archive, run with `includeUI`
 maven profile. `jberet-ui` module adds a front-end UI for interacting with 
 batch job data. The following command will clean, build, deploy, and run the tests:
 
 ```
 mvn clean install -PincludeUI
 ```
 
 To access `jberet-ui` web pages, go to http://localhost:8080/scheduleExecutor/, where you can 
 view, manage, or schedule job executions.
 
## Screenshot ([more](https://github.com/jberet/jsr352/issues/71#issuecomment-216072257)):

![scheduleExecutor sample screenshot](https://cloud.githubusercontent.com/assets/2079251/14944316/6ede6638-0fbd-11e6-923a-ab843ef23efc.png)