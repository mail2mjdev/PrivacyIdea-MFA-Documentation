## Setup and Configure SQLResolver

**SQL Database**
1. Setup & Install 
    [Link](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-16-04)

2. Configure MySQL
    `sudo cat /etc/mysql/debian.cnf`

    File will have:
    >host = localhost
    >user = debian-sys-maint
    >password = SqlUserpassword

    **Follow the steps below to reset the MySQL `root` user password:**

    ```
    # mysql -u debian-sys-maint -p
    Enter the password(enter)

    # mysql> USE mysql
    # mysql> UPDATE mysql.user SET Password=PASSWORD('NewSqlUserPassword') WHERE User='root';
    # mysql> FLUSH PRIVILEGES;
    # mysql> COMMIT;
    # mysql> EXIT;

    ```
    **Create Database and Table (for using in MFA sqlresolver):**

    ```
    # mysql> CREATE DATABASE mfadb;

    # mysql> CREATE TABLE Users
    (
        userid int NOT NULL AUTO_INCREMENT PRIMARY KEY,
        username varchar(255),
        phone varchar(255),
        mobile varchar(255),
        email varchar(255),
        surname varchar(255),
        givenname varchar(255),
        password varchar(255)
    );

    ```

    **Create a new SQL Resolver**
    
    * `Resolver name` : `AnyRosolverName`
    * `Driver`        : `mysql+pymsql`
    * `Server`        : `127.0.0.1` (local / Public IP)
    * `Port`          : `3306`
    * `Database`      : `mfadb` (create a db with the same name above, you should give your db name)
    * `User`          : `root` (default user of MySQL)
    * `Password`      : `NewSqlUserPassword` (Password you have configured)
    * `Table`         : `Users` (Name of table for storing the user records)
    * `Limit`         : `500`
    * `Mapping`       : `{"userid":"userid","username": "username", "phone" : "phone", "mobile" : "mobile", "email" : "email", "surname" : "surname", "givenname" : "givenname" ,"password" : "password"}`

    **Save SQL Resolver**
    > To test click on the button __Test SQL Resolver__
    > If settings and DB Mapping is correct, It will return no of users present in the DB.