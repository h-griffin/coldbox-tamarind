# Build a foundation app with Coldbox/Lucee/MySQL 5.7

## ======== INFO ===========

- java
- scripts - components  
- tags - views  

- coldbox is mvc 'model view controller' framework for CFML 'coldfusion markup language'
- coldbox for CFML = django for python

- command box 
    - command line
    - like npm for node js

- production deployments lightwieght docker image "minibox"

- quick orm
    - database commmunication
    - QB
        - inplace of SQL statement
        - schema builder with components
		- works with
			- mySQL
			- oracle
			- postgresSQL
			- microsoft SQL

## ===== PRE REQ =============

- command box 
    - Mac: homebrew 
    - install`> $ brew install commandbox` 
    - open/run `> $ box`
    - update `> $ brew upgrade commandbox`

- vsCode extensions
    - CFML syntax
    - comand box extension

- MySQL
    - 5.7 ( not 5.8)
    - sequeal pro on mac https://sequelpro.com/download
        - create db instance called `cbox1`
        - assign user credentials
            - root
            - webuser

## ====== CREATE COLDBOX PROJ ========
- dont need template
    - run `> $ coldbox create app myApp`
    - or within myApp folder `> $ coldbox create app`
    - both of these in the commandbox prompt will create proj in myApp folder
- with template
    - run `> $ coldbox create app skeleton=cbtemplate-{name}`
- this app uses `quick-with-auth` (Quick ORM and auth needed)
    - `> $ coldbox create app skeleton=cbtemplate-quick-with-auth`
    - *remember `rest`
    - this will auto install modules needed (cbGuard and bCrypt)
        - cbauth - user sessions
        - cbguard - access to handlers for unauthorized users
        - bCrypt - coldbox encryption 
        - cbValidation - input validation to rules
        - Commandbox-dotenv & commandbox-cfconfig - configuration
        - Commandbox-migration - database communication
        - verify-csrf-interceptor - check tokens on form submit
        - redirect-back uniqueInDatabase - validators
         

## ======== CREATE APP ==========
- in project folder cbox1 `~/udemy/c#/cbox1`
- `> $ box`
- `> $ coldbox create app skeleton=cbtemplate-quick-with-auth`
    - cftoken error is ok will not affect proj, is related to verify-csrf-interceptor

## ======= REVIEW INSTALLS ===========

- config/coldbox.cfc component
	- app settings
- config/router.cfc component
	- actions for get/set/create/remove
- interceptors 
	- components execute when conditions are met 
- /handlers work with the /views 
	- regestration & sessions
- rescorces/database/migrations
	- migrations log
	- /rescources where you put css templates and js components
- env
	- environments keys
- server.json
	- version of engine
- cfconfig.json
	- proper settings for when you connect to server
	- change in env if you cange settings
- application.cfc
	- default set up
- testbox
	- preinstall, dont touch
- test
	- specs for integration tests
	- test has different datasource than main app (mysql)

## ======= ENABLE THE PROJECT =========

- log into mysql
- create .env
- enable data migration
- create user table in db

- **config/coldbox.cfc**
	- module settings
		- `quick : { defaultGrammar = "MySQLGrammar@qb"},`

- **Application.cfc** (root)
	- change datascource from `coldbox`
		- `this.datasource = "cbox1";`

- **.env**
	- app name - cbox1
	- connectionstring - cbox1
	- database - cbox1
	- scema - cbox1
	- password - test

- enable schema migrations
	- `> $ box`
	- `> $ migrate install`

- setting up mysql on mac
	- `> $ /usr/local/mysql/bin/mysql -u root -p `
	- log in 
	- `mysql> create database cbox1;`
		- `mysql> CREATE USER 'admin'@'localhost';`
		- `mysql> create user 'root@localhost' identified by 'root'`
		- identify by : password
	- `mysql> GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';`
	- `mysql> SHOW DATABASES;`
	- cannot get connection

- migrate users table
	- rescources/database/migrations.cfc
	- migrate up - create schema
	- migrate down - delete schema

## ======= CONFIGURE LUCEE SERVER =========
- `> $ box`
- `> $ start cfengine=lucee@5`
- `> $ server list`

```
cbox1 (running)
  http://127.0.0.1:56061
  CF Engine: lucee 5.3.6+61
  Webroot: /Users/haleygriffin/udemy/c#/cbox1/
  Last Started: 27-Feb-2021 17:33:07
```
- server problems - boolean
    - **server.json**
        - rewrites {enable} remove "" must be bool not string
		- `"enable":true`
	- make a copy of file
	- add http port
		- `"http":{"port":56628}`
	- add name
		- `"name":"cbox1"`
	- update lucee version
		- `"cfengine":"lucee@3.6+61",`
		- leaving at generic 5 will overwrite server.json when new realease is out
	- reset server ('server start' and 'start' both work)
		- `> $ stop`
		- `> $ start`
	- server error ? 
		- `box install cbjavaloader`

- Lucee administration
	- icon at top of mac, by time stamp
	- use command box to set password
	- make sure module commandbox-config installed (latest version)
		- `> $ list` 
		- `> $ install commandbox-cfconfig`
		- `cfconfig set adminPassword=cbox1`
	- log in and verify cbox1 mysql datascource
	- server admon global settings
	- web admin local project settings
	