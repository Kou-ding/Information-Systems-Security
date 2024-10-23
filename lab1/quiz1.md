## Exercise 1
Ανοίξτε ένα cmd (στο φάκελο που είναι εγκατεστημένη η mysql) και κάντε login ως root με την εντολή:
```bash
mysql -u root -p
```
(η MySQL είναι στο φάκελο: C:\Program Files\MySQL\mysql\current\bin)

α) Εκτελέστε τις παρακάτω εντολές και δείτε τι κάνουν:
USE mysql;
DESCRIBE user;
Με ποια εντολή μπορούμε να δούμε τους χρήστες της MySQL;

β) Δημιουργήστε τους χρήστες admin<δικό σας AEM> (π.χ. admin10101) και user<δικό σας ΑΕΜ> με password: a123

γ) Επιβεβαιώστε τη δημιουργία τους (βλ. α)

δ) Μετονομάστε τον χρήστη admin ώστε να επιτρέπεται να συνδεθεί μόνο τοπικά.

ε) Αλλάξτε το password του χρήση admin σε: sec123

Καταγράψτε τις εντολές για τα α), β), δ), ε) και screenshot για τo γ)
### Solution
a)
```bash
USE mysql;
```
output:
```
Database changed
```

```bash
select user from mysql.user;
```
output:
```
+------------------+
| user             |
+------------------+
| user1            |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
| student          |
+------------------+
6 rows in set (0.01 sec)
```

```bash
select user,host,authentication_string from user;
```
output:
```
+------------------+-----------+------------------------------------------------------------------------+
| user             | host      | authentication_string                                                  |
+------------------+-----------+------------------------------------------------------------------------+
| user1            | %         | $A$005$☺aH^7¶↓blwrgTJ*▲        ‼AM7ezIDFDUfZn5xH081MagFPRxhI52OIHXu1C8Yb5a7A5 |
| mysql.infoschema | localhost | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED |
| mysql.session    | localhost | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED |
| mysql.sys        | localhost | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED |
| root             | localhost |                                                                        |
| student          | localhost | $A$005$♀
y↕H%;e*A<♫c}.nz;^6/ZTFjyRESNnVAmSSx3iHOcAZ6.lJ0KD0YgNHeMbiTY3 |
+------------------+-----------+------------------------------------------------------------------------+
6 rows in set (0.01 sec)
```

```bash
describe user;
```
output:
```
+--------------------------+-----------------------------------+------+-----+-----------------------+-------+
| Field                    | Type                              | Null | Key | Default               | Extra |
+--------------------------+-----------------------------------+------+-----+-----------------------+-------+
| Host                     | char(255)                         | NO   | PRI |                       |       |
| User                     | char(32)                          | NO   | PRI |                       |       |
| Select_priv              | enum('N','Y')                     | NO   |     | N                     |       |
| Insert_priv              | enum('N','Y')                     | NO   |     | N                     |       |
| Update_priv              | enum('N','Y')                     | NO   |     | N                     |       |
| Delete_priv              | enum('N','Y')                     | NO   |     | N                     |       |
| Create_priv              | enum('N','Y')                     | NO   |     | N                     |       |
| Drop_priv                | enum('N','Y')                     | NO   |     | N                     |       |
| Reload_priv              | enum('N','Y')                     | NO   |     | N                     |       |
| Shutdown_priv            | enum('N','Y')                     | NO   |     | N                     |       |
| Process_priv             | enum('N','Y')                     | NO   |     | N                     |       |
| File_priv                | enum('N','Y')                     | NO   |     | N                     |       |
| Grant_priv               | enum('N','Y')                     | NO   |     | N                     |       |
| References_priv          | enum('N','Y')                     | NO   |     | N                     |       |
| Index_priv               | enum('N','Y')                     | NO   |     | N                     |       |
| Alter_priv               | enum('N','Y')                     | NO   |     | N                     |       |
| Show_db_priv             | enum('N','Y')                     | NO   |     | N                     |       |
| Super_priv               | enum('N','Y')                     | NO   |     | N                     |       |
| Create_tmp_table_priv    | enum('N','Y')                     | NO   |     | N                     |       |
| Lock_tables_priv         | enum('N','Y')                     | NO   |     | N                     |       |
| Execute_priv             | enum('N','Y')                     | NO   |     | N                     |       |
| Repl_slave_priv          | enum('N','Y')                     | NO   |     | N                     |       |
| Repl_client_priv         | enum('N','Y')                     | NO   |     | N                     |       |
| Create_view_priv         | enum('N','Y')                     | NO   |     | N                     |       |
| Show_view_priv           | enum('N','Y')                     | NO   |     | N                     |       |
| Create_routine_priv      | enum('N','Y')                     | NO   |     | N                     |       |
| Alter_routine_priv       | enum('N','Y')                     | NO   |     | N                     |       |
| Create_user_priv         | enum('N','Y')                     | NO   |     | N                     |       |
| Event_priv               | enum('N','Y')                     | NO   |     | N                     |       |
| Trigger_priv             | enum('N','Y')                     | NO   |     | N                     |       |
| Create_tablespace_priv   | enum('N','Y')                     | NO   |     | N                     |       |
| ssl_type                 | enum('','ANY','X509','SPECIFIED') | NO   |     |                       |       |
| ssl_cipher               | blob                              | NO   |     | NULL                  |       |
| x509_issuer              | blob                              | NO   |     | NULL                  |       |
| x509_subject             | blob                              | NO   |     | NULL                  |       |
| max_questions            | int unsigned                      | NO   |     | 0                     |       |
| max_updates              | int unsigned                      | NO   |     | 0                     |       |
| max_connections          | int unsigned                      | NO   |     | 0                     |       |
| max_user_connections     | int unsigned                      | NO   |     | 0                     |       |
| plugin                   | char(64)                          | NO   |     | caching_sha2_password |       |
| authentication_string    | text                              | YES  |     | NULL                  |       |
| password_expired         | enum('N','Y')                     | NO   |     | N                     |       |
| password_last_changed    | timestamp                         | YES  |     | NULL                  |       |
| password_lifetime        | smallint unsigned                 | YES  |     | NULL                  |       |
| account_locked           | enum('N','Y')                     | NO   |     | N                     |       |
| Create_role_priv         | enum('N','Y')                     | NO   |     | N                     |       |
| Drop_role_priv           | enum('N','Y')                     | NO   |     | N                     |       |
| Password_reuse_history   | smallint unsigned                 | YES  |     | NULL                  |       |
| Password_reuse_time      | smallint unsigned                 | YES  |     | NULL                  |       |
| Password_require_current | enum('N','Y')                     | YES  |     | NULL                  |       |
| User_attributes          | json                              | YES  |     | NULL                  |       |
+--------------------------+-----------------------------------+------+-----+-----------------------+-------+
51 rows in set (0.00 sec)
```

b)

```bash
create user admin10371 identified by '10371';
```
output:
```
Query OK, 0 rows affected (0.13 sec)
```

```bash
create user user10371 identified by '10371';
```
output:
```
Query OK, 0 rows affected (0.02 sec)
```

c)

```bash
select user,host from user;
```
output:
```
+------------------+-----------+
| user             | host      |
+------------------+-----------+
| admin10371       | %         |
| user1            | %         |
| user10371        | %         |
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| root             | localhost |
| student          | localhost |
+------------------+-----------+
8 rows in set (0.00 sec)
```

d)

```bash
rename user admin10371 to admin10371@localhost;
```
output:
```
Query OK, 0 rows affected (0.02 sec)
```
```bash
select user,host from user;
```
output:
```
+------------------+-----------+
| user             | host      |
+------------------+-----------+
| user1            | %         |
| user10371        | %         |
| admin10371       | localhost |
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| root             | localhost |
| student          | localhost |
+------------------+-----------+
8 rows in set (0.00 sec)
```

e)
```bash
alter user user10371 identified by 'sec123';
```
output:
```
Query OK, 0 rows affected (0.02 sec)
```
## Exercise 2
Δημιουργήστε μια νέα ΒΔ με όνομα mydb<δικό σας ΑΕΜ>
(tip: CREATE DATABASE …)

α) Αλλάξτε την ενεργή ΒΔ και δημιουργήστε ένα νέο πίνακα στην παραπάνω ΒΔ με όνομα clients με τις παρακάτω εντολές:

CREATE TABLE clients (
   id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
   name VARCHAR(50) NOT NULL UNIQUE,
   tel VARCHAR(50) DEFAULT '(01)-23456789',
   credit FLOAT NOT NULL DEFAULT 0 CHECK (credit >= 0)
);

β) Με ποιά εντολή μπορείτε να δείτε το schema του πίνακα που κάνατε;

γ) Δημιουργήστε μια ΌΨΗ (VIEW) με όνομα v_clients για τον παραπάνω πίνακα που να περιέχει μόνο τα πεδία name και tel

Καταγράψτε τις εντολές για τα β), γ) και screenshot για τo α)
### Solution
a)
```bash
create database mydb10371;
```
output:
```
Query OK, 1 row affected (0.12 sec)
```
```bash
use mydb10371;
```
output:
```
Database changed
```
```bash
CREATE TABLE clients (
    ->    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    ->    name VARCHAR(50) NOT NULL UNIQUE,
    ->    tel VARCHAR(50) DEFAULT '(01)-23456789',
    ->    credit FLOAT NOT NULL DEFAULT 0 CHECK (credit >= 0)
    -> );
```
output:
```
Query OK, 0 rows affected (0.14 sec)
```
b)
```bash
describe clients;
```
```
+--------+-------------+------+-----+---------------+----------------+
| Field  | Type        | Null | Key | Default       | Extra          |
+--------+-------------+------+-----+---------------+----------------+
| id     | int         | NO   | PRI | NULL          | auto_increment |
| name   | varchar(50) | NO   | UNI | NULL          |                |
| tel    | varchar(50) | YES  |     | (01)-23456789 |                |
| credit | float       | NO   |     | 0             |                |
+--------+-------------+------+-----+---------------+----------------+
4 rows in set (0.01 sec)
```
c)
```bash
create view v_clients as
    -> select name,tel from clients;
```
output:
```
Query OK, 0 rows affected (0.04 sec)
```

```bash
describe v_clients;
```
output:
```
+-------+-------------+------+-----+---------------+-------+
| Field | Type        | Null | Key | Default       | Extra |
+-------+-------------+------+-----+---------------+-------+
| name  | varchar(50) | NO   |     | NULL          |       |
| tel   | varchar(50) | YES  |     | (01)-23456789 |       |
+-------+-------------+------+-----+---------------+-------+
2 rows in set (0.00 sec)
```
## Exercise 3
Δημιουργήστε δύο ρόλους για την ΒΔ που κάνατε σύμφωνα με τα παρακάτω

α) Δημιουργήστε τους παρακάτω ρόλους:

 r_admin<ΑΕΜ>: με όλα τα δικαιώματα σε ολόκληρη τη ΒΔ που κάνατε (την mydb...)
 r_reader<ΑΕΜ>: με δικαίωμα ανάγνωσης μόνο στην όψη που κάνατε

β) Αποδώστε το ρόλο r_admin<ΑΕΜ> στον χρήστη admin<ΑΕΜ>
    και τον ρόλο r_reader<ΑΕΜ> στον χρήστη user<ΑΕΜ>

γ) Με ποιά εντολή μπορείτε να δείτε τα δικαιώματα που δώσατε;

 Καταγράψτε τις εντολές για τα α), β), γ) και screenshot για τo γ)
### Solution
a)
```bash
mysql> create role r_admin10371,r_reader10371;
```
output:
```
Query OK, 0 rows affected (0.02 sec)
```

```bash
mysql> grant all on mydb10371 to r_admin10371;
```
output:
```
Query OK, 0 rows affected (0.02 sec)
```

```bash
mysql> grant select on mydb10371.* to r_reader10371;
```
output:
```
Query OK, 0 rows affected (0.01 sec)
```

b)
```bash
grant r_admin10371 to admin10371@localhost;
```
output:
```
Query OK, 0 rows affected (0.02 sec)
```

```bash
grant r_reader10371 to user10371;
```
output:
```
Query OK, 0 rows affected (0.01 sec)
```

c)
```bash
show grants for admin10371@localhost;
```
output:
```
+------------------------------------------------------+
| Grants for admin10371@localhost                      |
+------------------------------------------------------+
| GRANT USAGE ON *.* TO `admin10371`@`localhost`       |
| GRANT `r_admin10371`@`%` TO `admin10371`@`localhost` |
+------------------------------------------------------+
2 rows in set (0.00 sec)
```

```bash
show grants for user10371;
```
output:
```
+----------------------------------------------+
| Grants for user10371@%                       |
+----------------------------------------------+
| GRANT USAGE ON *.* TO `user10371`@`%`        |
| GRANT `r_reader10371`@`%` TO `user10371`@`%` |
+----------------------------------------------+
2 rows in set (0.00 sec)
```

## Exercise 4
α) Κάντε login ως admin<AEM>, αλλάξτε την ενεργή ΒΔ (εντολή: USE mydb<AEM>;) και δοκιμάστε να εισάγετε κάποια δοκιμαστικά δεδομένα στον πίνακα με την εντολή:

INSERT INTO clients (name, tel, credit) VALUES
   ('full name1', '867483930', 50),
   ('full name2', '987654321', 100),
   ('full name3', '147852369', 1000);

 (tip: μετά το κάθε login θα πρέπει να ενεργοποιείτε τον ρόλο σας, εντολή: SET ROLE όνομα_ρόλου;)

  β) Κάντε login ως user, αλλάξτε την ενεργή ΒΔ (εντολή: USE mydb<AEM>;) και δείτε ποιους πίνακες βλέπετε (εντολή: SHOW TABLES;).

- Διαβάστε όλες τις εγγραφές του πίνακα που έχετε δικαιώματα ανάγνωσης.

γ) Ανακαλέστε (REVOKE) το δικαίωμα εισαγωγής εγγραφών (INSERT) από τον ρόλο r_admin+ΑΕΜ.

- Μπείτε σαν admin και δοκιμάστε να κάνετε εισαγωγή νέας εγγραφής ως admin, π.χ. με την εντολή:

INSERT INTO clients (name, tel, credit) VALUES ('full name4', '0202020202', 150);

### Solution

## Exercise 5
Ακυρώστε τις αλλαγές που κάνατε ακολουθώντας τα παρακάτω βήματα:

α) Διαγράψτε τους ρόλους: r_admin<AEM> και r_user<AEM>

β) Διαγράψτε τη ΒΔ που φτιάξατε mydb<AEM>

γ) Διαγράψτε τους χρήστες: admin<AEM> και user<AEM>

Καταγράψτε τις εντολές που χρησιμοποιήσατε

### Solution