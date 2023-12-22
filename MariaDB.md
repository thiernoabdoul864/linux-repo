# Introduction to MariaDB
MariaDB is a database server available in RHEL / CentOS systems.It is a fork of the MySQL Database.All the commands used in MySQL DB can be used in MariaDB as well.It is an open source Database system.To interface with the MariaDB server, the default client program "mysql" is used.Using this client program, commands can be executed in the command line
or we can enter into terminal mode.
###  Basics information about MariaDB
`Package: mariadb-server`
`Daemon: mariadb`
 ### Configuring MariaDB
The MariaDB serve can be configured in RHEL / CentOS system by following the below steps.
### Step 1: Install the package
The package to be installed for using mariadb service is 
`"mariadb-server"`. 
It can be installed using yum.
`yum install -y mariadb-server` 
This package also installs many other dependent packages out of which the following are not to be ignored: 

`mariadb-5.5.52-1.el7.x86_64 - MySQL client programs and utilities` `mariadb-server-5.5.52-1.el7.x86_64 - Actual MariaDB MySQL database server.`
 ### Step 2: Start and enable the service
Start and enable the "mariadb" service.

`systemctl enable --now mariadb` 

### Step 3: Connect to the Database
Connect to the MariaDB using the client program, "mysql" as follows: 

`mysql -u root` 

You are now successfully taken to the MariaDB terminal where you an perform all MySQL related operations like creating, delete or alter a database and tables.Step 4: Performing MySQL operations In the MariaDB terminal, any mysql operations can be performed since it is a fork of the original MySQL database.Also, the "mycsql" client program installed as dependency enables us to interact with the server.###  To show the available database:
`show databases ;` 
 ### To create a new database:
    `CREATE DATABASE employee;`
     ### To use the created database:
    `USE employee;` 
    ###  Create a new table in the database:

   
    CREATE TABLE teachers (
        teacher_id INT PRIMARY KEY AUTO_INCREMENT,
        name VARCHAR(255),
        subject VARCHAR(255),
        experience_years INT
    );
-- Inserting three records
INSERT INTO teachers (teacher_id, name, subject, experience_years)
VALUES (1, 'John Doe', 'Math', 5),
    (2, 'Jane Smith', 'Science', 8),
    (3, 'Bob Johnson', 'History', 3);

###  Get table details:
`DESCRIBE teachers ;` 
### Selecting all records from the 'teachers' table

`SELECT * FROM teachers;` 

Along with this, every other mysql operations can be performed in the mariadb server.
Once done, you can exit from the mariadb server terminal by typing 
`exit`.