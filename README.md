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
    In this repository I'm sharing some of what I've been learning about Spring Boot with 
   <a href="https://docs.liquibase.com/tools-integrations/springboot/springboot.html">Liquibase.</a> By following the instructions and reading the code I hope I can contribute to your development. Good studies. :coffee: 
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

We may use one or more migration files as long as the other files are configured in the main file. In the example done, I tried to organize in different directories and using different format files. That way we can make the project more organized confirm example below.

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
The file *changelog-master.xml* includes new files where our migration instructions are.

![a](https://user-images.githubusercontent.com/23198970/179365703-d6b2e4a9-ed63-4c8a-afec-2b8ae22c2daf.png)

```yaml
#create.yaml
databaseChangeLog:
  - changeSet:
      id: 2
      author: Kalistonss
      changes:
        - createTable:
            tableName: tb_users
            columns:
              - column:
                  name: id
                  type: int
                  autoIncrement: true
                  constraints:
                    primaryKey: true
                    nullable: false
              - column:
                  name: name
                  type: varchar(100)
              - column:
                  name: email
                  type: varchar(100)
                  constraints:
                    nullable: false

```
This sample also enables the H2 console (at `http://localhost:8080/api/h2-console`) so that you can review the state of the database (the default jdbc url is jdbc:h2:mem:hbasedb).


##### Thanks :call_me_hand:
 [![LinkedIn][linkedin-shield]][linkedin-url]
 
 
 
 [instagram-shield]: https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white
[instagram-url]: https://www.instagram.com/kaliston_s/
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/kalistonss/
