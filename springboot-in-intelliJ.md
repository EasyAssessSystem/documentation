# Work with SpringBoot + HibernateJPA + Maven in IntelliJ

## 1. Install Maven
```sh
   brew install maven
```

## 2. Create New Project in IntelliJ
   1) Choose type 'Spring Initializr'
   
   2) Select local JDK
   
   3) Use Maven as the project type
   
   4) Enter artifact name with specific format easyassess-{project_name} (i.e easyassess-pdm) and enter package name as
      com.stardust.easyassess.{project_name}. Use com.stardust.easyassess as the group id
## 3. Select dependencies 
   NOTE: you can add dependencies manually after you created the project, but I recommend to choose all your needs in 
   
   advanced otherwise you have to reflush repository from command line. Below are the options I suggest to choose.
   
   1) Core section
```  
  * AOP
  * DevTools
  * Validation
  * Session
```
   2) Web section
```  
  * Web
  * REST docs
  * JAX-RS
```      
   3) SQL
```
  * JPA
  * JDBC
  * MySQL
  * HSQLDB
  * H2
```
   4) No-SQL
```
  * MongoDB
  * Redis
  * ElasticSearch
```
      
## 4. Enter project name and directory then finish the project creation.
## 5. Initialize the application.properties file (under {project}\src\main\resources)
```
  spring.datasource.url = jdbc:mysql://{host_address}:3306/{database_name}
  spring.datasource.username = {username}
  spring.datasource.password = {password}
  spring.datasource.driverClassName = com.mysql.jdbc.Driver
  # Specify the DBMS
  spring.jpa.database = MYSQL
  # Show or not log for each sql query
  spring.jpa.show-sql = true
  # Hibernate ddl auto (create, create-drop, update)
  spring.jpa.hibernate.ddl-auto = update
  # Naming strategy
  spring.jpa.hibernate.naming-strategy = org.hibernate.cfg.ImprovedNamingStrategy
  # stripped before adding them to the entity manager)
  spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5Dialect
```
## 6. Create package com.stardust.easyassess.{project_name}.beans in java folder
   
   Add a entity class for test purpose, following example is a typical JPA ORM standard.
```java
@Entity
@Table(name="Users")
public class User {

    private long id;

    private String name;

    @Id
    @GeneratedValue
    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

}
```
## 7. Create a controller package in java folder com.stardust.easyassess.{project_name}.controllers
```java
@RestController
public class UserController {
    @RequestMapping("/user")
    public User home() {
        User u = new User();
        u.setId(1);
        u.setName("Test");
        return u;
    }
}
```

```
visit http://localhost:8080/user to test it
```

