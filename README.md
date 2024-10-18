# MicroWebServer


Quick Start
------------
* Server Test Environment
    * Ubuntu v16.04
    * MySQL v5.7.29
* Browser Test Environment
    * Windows or Linux
    * Chrome
    * FireFox
    * Other browsers not yet tested

* Ensure MySQL database is installed before testing

    ```C++
    // Create the yourdb database
    create database yourdb;

    // Create user table
    USE yourdb;
    CREATE TABLE user(
        username char(50) NULL,
        passwd char(50) NULL
    )ENGINE=InnoDB;

    // Add data
    INSERT INTO user(username, passwd) VALUES('name', 'passwd');
    ```

* Modify the database initialization information in main.cpp

    ```C++
    // Database username, password, and database name
    string user = "root";
    string passwd = "root";
    string databasename = "yourdb";
    ```

* Build

    ```C++
    sh ./build.sh
    ```

* Start server

    ```C++
    ./server
    ```

* Browser

    ```C++
    ip:9006
    ```

Customized Run
------

```C++
./server [-p port] [-l LOGWrite] [-m TRIGMode] [-o OPT_LINGER] [-s sql_num] [-t thread_num] [-c close_log] [-a actor_model]
```

Friendly reminder: The above parameters are not mandatory, you can choose them according to your needs.

* -p, custom port number
    * Default is 9006
* -l, select log writing method, default is synchronous write
    * 0, synchronous write
    * 1, asynchronous write
* -m, combination of listenfd and connfd modes, default is LT + LT
    * 0, indicates LT + LT
    * 1, indicates LT + ET
    * 2, indicates ET + LT
    * 3, indicates ET + ET
* -o, graceful shutdown of connections, default is not used
    * 0, do not use
    * 1, use
* -s, number of database connections
    * Default is 8
* -t, number of threads
    * Default is 8
* -c, close logs, default is open
    * 0, open logs
    * 1, close logs
* -a, select Reactor model, default is Proactor
    * 0, Proactor model
    * 1, Reactor model

Test Example Command and Meaning

```C++
./server -p 9007 -l 1 -m 0 -o 1 -s 10 -t 10 -c 1 -a 1
```

- [x] Port 9007
- [x] Asynchronous log writing
- [x] LT + LT combination
- [x] Graceful shutdown of connections
- [x] 10 database connections in the pool
- [x] 10 threads in the thread pool
- [x] Logs are closed
- [x] Reactor model
