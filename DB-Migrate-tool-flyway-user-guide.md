# What is the flyway
flyway is the tool we used to control database version and database migration.you can see the link [here](https://flywaydb.org)

## Installation
To install flyway for mac user there are two options:
1. install by brew
```sh
	brew install flyway
```
2. Download the source and extract it in you machine. to get the file you can access here:[flyway download](https://flywaydb.org/documentation/commandline/)

## configuration
if you install from zip file, To use flyway,you should add the filepath to your PATH.

```sh
	export PATH=<you flyway filepath>:$PATH
```
after that you can try to type "flyway" in your terminal. 

To configure flyway you should locate the conf file in you flyway installed location.here is the example path:
```sh
/Users/abcdef/flyway-4.0.1/conf/flyway.conf
```
there are some import setting you should make in the conf file.

```sh
	flyway.url=jdbc:mysql://localhost:3306/databasename?useUnicode=true&amp;characterEncoding=utf-8
	flyway.user=root
	flyway.password=
	flyway.locations=filesystem:<your dbsql location>
```
Since we use mysql for development, the above is the mysql example.

## How to use 
flyway use sql to track your database version.By default it search the sql forder in your flyway installed location to find the migration information.


### Migrate
For example:
1. create the first migration in the sql folder created and file named:V1__Create_person_table.sql
```sql
	create table PERSON (
    ID int not null,
    NAME varchar(100) not null
);
```

excute this to run the migration

```sh
		flyway migrate
```

2. create the second migrat,create a file called V2__Add_people.sql
```sql
insert into PERSON (ID, NAME) values (1, 'Axel');
insert into PERSON (ID, NAME) values (2, 'Mr. Foo');
insert into PERSON (ID, NAME) values (3, 'Ms. Bar');
```

excute this to run the migration

```sh
	flyway migrate
```
PS.注意sql的文件名是**两个下划线**,同时sql文件的命名已V1__xxxx.sql来命名，V表示版本，1代表版本号。


### Rollback
if you made some mistake and created an wrong db migration and would like to back to eariler version. you can see this command.
```sh
	flyway repair
```
### Info
if you would like to get the version history of your db migration you can use this command.
```sh
	flyway Info
```

### changet the migration sql folder
By default flyway search the sql folder under flyway installation path to find the migration sql. buy you can change it to your specify path. change the locations in flyway.conf file.

```sh
	flyway.locations=filesystem:<your dbsql location>
```










