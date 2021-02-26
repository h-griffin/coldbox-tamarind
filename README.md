Build a foundation app with Coldbox/Lucee/MySQL 5.7


java
scripts - components  
tags - views  

coldbox is mvc 'model view controller' framework for CFML

coldbox for CFML = django for python

command box 
    command line
    like npm for node js

production deployments lightwieght docker image "minibox"

========INFO===========
quick orm
    database commmunication
    QB
        inplace of SQL statement
        schema builder with components

        mySQL
        oracle
        postgresSQL
        microsoft SQL

=====PRE REQ=============

command box 
    Mac: homebrew 
    install`> $ brew install commandbox` 
    open/run `> $ box`
    upgrade `> $brew upgrade commandbox`

extensions
    CFML syntax
    comand box extension

MySQL
    5.7 ( not 5.8)
    sequeal pro on mac https://sequelpro.com/download
        create db instance called `cbox1`
        assign user credentials
            root
            webuser

====== CREATE COLBOX PROJ ========
dont need template
    run `> $ coldbox create app myApp`
    or within myApp folder `> $ coldbox create app`
    both of these in the commandbox prompt will create proj in myApp folder
with template
    run `> $ coldbox create app skeleton=cbtemplate-{name}`
this app uses `quick-with-auth` (Quick ORM and auth needed)
    `> $ coldbox create app skeleton=cbtemplate-quick-with-auth`
    *remember `rest`
    this will auto install modules needed (cbGuard and bCrypt)
        cbauth - user sessions
        cbguard - access to handlers for unauthorized users
        bCrypt - coldbox encryption 
        cbValidation - input validation to rules
        Commandbox-dotenv & commandbox-cfconfig - configuration
        Commandbox-migration - database communication
        verify-csrf-interceptor - check tokens on form submit
        redirect-back uniqueInDatabase - validators
         

========CREATE APP==========
in project folder cbox1 `~/udemy/c#/cbox1`
`> $ box`
`> $ coldbox create app skeleton=cbtemplate-quick-with-auth`
    cftoken error is ok will not affect proj, is related to verify-csrf-interceptor

