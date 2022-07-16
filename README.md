<div id="top" align="center">
  <h1> Demo Spring Boot with Liquibase and H2 </h1>
</div>

<div align="center">
  <a>
    <img src="image/logo.jpg" alt="Logo" width="270" height="120">
  </a>
</div>
</br>
  <div align="start">
    In this repository I'm sharing some of what I've been learning about Spring Boot with Liquibase. By following the instructions and reading the code I hope I can contribute to your development. Good studies. :coffee: 
  </div>
  <h3 align="start">
    Go to <a href="https://start.spring.io/">Spring Initializr</a>, configure and add the dependencies.
  </h3>
  <div align="start">
    1. Spring Web </br>
    2. Spring Data JPA </br>
    3. H2 Database </br>
    4. Liquibase Migration </br>
  </div>

#### Configuration

After you import the project, navigate to the properties file of your application. Configure the accesses to the database and the location where Spring should fetch the *changelog* file from Liquibase. The supported files are: </br>
> .xml  </br>
> .yaml  </br>
> .json  </br>
> .sql  </br>

###### Example.

```
spring:
  liquibase:
    change-log: classpath:db/changelog/changelog-master.xml
```

We can use one or more migration files as long as the other files are configured in the main file. In the example done, I tried to organize in different directories and using different format files. That way we can make the project more organized confirm example below.

```
 <!--    changelog-master.xml -->
<databaseChangeLog
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
        xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
         http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd">

   
    <changeSet id="1" author="kalistonss">
        <validCheckSum></validCheckSum>
        <sqlFile path="db/changelog/book/create.sql"/>
    </changeSet>
    <changeSet id="3" author="kalistonss">
        <validCheckSum></validCheckSum>
        <sqlFile path="db/changelog/book/insert.sql"/>
    </changeSet>
    <include file="db/changelog/user/create.yaml" />
    <include file="db/changelog/user/insert.yaml" />

</databaseChangeLog>
```
