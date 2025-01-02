### - MySQL 실행

```bash
jihyeokbae@MacBook-Pro-2 ~ % mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1034
Server version: 9.0.1 Homebrew

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

### - MySQL 구조

![image](https://github.com/user-attachments/assets/f3588358-5e27-44ba-8bfb-e5919e695610)

데이터들은 저렇게 표 형태로 저장된다. 그런데 이것들이 많아지게 되면 관리해야할 필요성이 생긴다.<br>
이런 표들을 그룹핑하는 것을 스키마(데이터베이스)라고 하고 일종에 폴더 같은 개념이다.

이런 스키마와 테이블을 저장하고 관리하는 것이 데이터베이스 서버이다. 이것은 MySQL 프로그램 자체를 의미한다.

### - MySQL 서버 접속, 데이터베이스 보안과 사용자 권한

MySQL은 파일과 달리 보안이 좋다. 또한 사용자별로 접근 권한도 부여할 수 있다.

1.  **MySQL 서버 접속 명령어**
    *   `mysql -u root -p`: root 사용자로 MySQL 서버에 접속하는 명령어
2.  **root 사용자:**
    *   관리자 권한을 가지며, 데이터베이스의 모든 작업에 대한 권한을 가진다.
    *   실제 시스템에서는 root 사용자로 직접 데이터베이스를 다루는 것은 위험하므로, 별도의 사용자를 만들어 작업하는 것이 권장된다.
    *   root 사용자는 중요한 작업을 수행할 때만 사용하는 것이 좋다.

MySQL 서버에 접속할 때 비밀번호를 입력해야 하는데 이때 성공적으로 접속하면, 이제 데이터베이스 서버라는 ‘담장’을 넘은 것과 같다.
### - MySQL 스키마 사용

```sql
mysql> CREATE DATABASE opentutorials;
Query OK, 1 row affected (0.00 sec)
```

스키마를 만드는 방법이다. 세미콜론을 붙여야 한다. 암기할 필요가 없다, 검색하면 다 나오니까...

![image](https://github.com/user-attachments/assets/6c8aa135-c8b9-4fff-b4cf-148ef6f850ba)
![image](https://github.com/user-attachments/assets/c9a49df6-4d56-4bff-947f-32d1f5e568a8)

이제 스키마에서 표를 만들 수 있게 되었다.

### - SQL과 테이블 구조

SQL은 **Structured Query Language**의 약자이다.

*   **Structured:** 구조화된 데이터를 조작하는데 특화
*   **Query:** "~에서 ~를 가져와라"와 같이 질의하는 것
*   **Language:** 컴퓨터와 데이터베이스 간의 의사소통을 위한 언어

![image](https://github.com/user-attachments/assets/30ab1ff7-b452-48a8-b5de-c12ef6541e3b)

테이블은 위와 같은 구조를 가진다.

### - MySQL 테이블의 생성

![image](https://github.com/user-attachments/assets/6d6e949d-80ee-495d-924f-5f2d3b61ae0c)

```sql
mysql> CREATE TABLE topic(
    ->  id INT(11) NOT NULL AUTO_INCREMENT,
    ->  title VARCHAR(100) NOT NULL,
    ->  description TEXT NULL,
    ->  created VARCHAR(15) NULL,
    ->  profile VARCHAR(200) NULL,
    ->  PRIMARY KEY(id));
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> SHOW TABLES;
+-------------------------+
| Tables_in_opentutorials |
+-------------------------+
| topic                   |
+-------------------------+
1 row in set (0.01 sec)

mysql> DROP TABLE topic;
Query OK, 0 rows affected (0.02 sec)

mysql> SHOW TABLES;
Empty set (0.00 sec)

mysql> CREATE TABLE topic(  id INT(11) NOT NULL AUTO_INCREMENT,  title VARCHAR(100) NOT NULL,  description TEXT NULL,  created VARCHAR(15) NULL,  profile VARCHAR(200) NULL,  PRIMARY KEY(id));
Query OK, 0 rows affected, 1 warning (0.02 sec)

mysql> SHOW TABLES;
+-------------------------+
| Tables_in_opentutorials |
+-------------------------+
| topic                   |
+-------------------------+
1 row in set (0.00 sec)
```
암기x. 검색으로 해결하면 된다.

아...저자를 넣지 않아 테이블을 수정한다.

```sql
mysql> CREATE TABLE topic(
    ->  id INT(11) NOT NULL AUTO_INCREMENT,
    ->  title VARCHAR(100) NOT NULL,
    ->  description TEXT NULL,
    ->  created DATETIME NOT NULL,
    ->  author VARCHAR(30) NULL,
    ->  profile VARCHAR(100) NULL,
    ->  PRIMARY KEY(id));
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> SHOW TABLES;
+-------------------------+
| Tables_in_opentutorials |
+-------------------------+
| topic                   |
+-------------------------+
1 row in set (0.01 sec)
```

### - MySQL CRUD

```sql
mysql> SHOW TABLES;
+-------------------------+
| Tables_in_opentutorials |
+-------------------------+
| topic                   |
+-------------------------+
1 row in set (0.01 sec)

mysql> DESC topic;
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| id          | int          | NO   | PRI | NULL    | auto_increment |
| title       | varchar(100) | NO   |     | NULL    |                |
| description | text         | YES  |     | NULL    |                |
| created     | datetime     | NO   |     | NULL    |                |
| author      | varchar(30)  | YES  |     | NULL    |                |
| profile     | varchar(100) | YES  |     | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
6 rows in set (0.01 sec)

mysql> INSERT INTO topic (title, description, created, author, profile) VALUES ('MySQL', 'MySQL is ...', NOW(), 'jihyeok', 'developer');
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM topic;
+----+-------+--------------+---------------------+---------+-----------+
| id | title | description  | created             | author  | profile   |
+----+-------+--------------+---------------------+---------+-----------+
|  1 | MySQL | MySQL is ... | 2024-12-28 13:59:29 | jihyeok | developer |
+----+-------+--------------+---------------------+---------+-----------+
1 row in set (0.00 sec)

mysql> INSERT INTO topic (title, description, created, author, profile) VALUES ('ORACLE', 'ORACLE is ...', NOW(), 'jihyeok', 'developer');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO topic (title, description, created, author, profile) VALUES ('SQL Server', 'SQL Server is ...', NOW(), 'duru', 'data administrator');
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO topic (title, description, created, author, profile) VALUES ('PostgreSQL', 'PostgreSQL Server is ...', NOW(), 'taeho', 'data scientist, developer');
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM topic;
+----+------------+--------------------------+---------------------+---------+---------------------------+
| id | title      | description              | created             | author  | profile                   |
+----+------------+--------------------------+---------------------+---------+---------------------------+
|  1 | MySQL      | MySQL is ...             | 2024-12-28 13:59:29 | jihyeok | developer                 |
|  2 | ORACLE     | ORACLE is ...            | 2024-12-28 14:01:26 | jihyeok | developer                 |
|  3 | SQL Server | SQL Server is ...        | 2024-12-28 14:02:27 | duru    | data administrator        |
|  4 | PostgreSQL | PostgreSQL Server is ... | 2024-12-28 14:03:19 | taeho   | data scientist, developer |
+----+------------+--------------------------+---------------------+---------+---------------------------+
4 rows in set (0.00 sec)
```

```sql
mysql> SELECT * FROM topic;
+----+-------+--------------+---------------------+---------+-----------+
| id | title | description  | created             | author  | profile   |
+----+-------+--------------+---------------------+---------+-----------+
|  1 | MySQL | MySQL is ... | 2024-12-28 13:59:29 | jihyeok | developer |
+----+-------+--------------+---------------------+---------+-----------+
1 row in set (0.00 sec)

mysql> INSERT INTO topic (title, description, created, author, profile) VALUES ('ORACLE', 'ORACLE is ...', NOW(), 'jihyeok', 'developer');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO topic (title, description, created, author, profile) VALUES ('SQL Server', 'SQL Server is ...', NOW(), 'duru', 'data administrator');
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO topic (title, description, created, author, profile) VALUES ('PostgreSQL', 'PostgreSQL Server is ...', NOW(), 'taeho', 'data scientist, developer');
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM topic;
+----+------------+--------------------------+---------------------+---------+---------------------------+
| id | title      | description              | created             | author  | profile                   |
+----+------------+--------------------------+---------------------+---------+---------------------------+
|  1 | MySQL      | MySQL is ...             | 2024-12-28 13:59:29 | jihyeok | developer                 |
|  2 | ORACLE     | ORACLE is ...            | 2024-12-28 14:01:26 | jihyeok | developer                 |
|  3 | SQL Server | SQL Server is ...        | 2024-12-28 14:02:27 | duru    | data administrator        |
|  4 | PostgreSQL | PostgreSQL Server is ... | 2024-12-28 14:03:19 | taeho   | data scientist, developer |
+----+------------+--------------------------+---------------------+---------+---------------------------+
4 rows in set (0.00 sec)

mysql> SELECT id,title,created,author FROM topic;
+----+------------+---------------------+---------+
| id | title      | created             | author  |
+----+------------+---------------------+---------+
|  1 | MySQL      | 2024-12-28 13:59:29 | jihyeok |
|  2 | ORACLE     | 2024-12-28 14:01:26 | jihyeok |
|  3 | SQL Server | 2024-12-28 14:02:27 | duru    |
|  4 | PostgreSQL | 2024-12-28 14:03:19 | taeho   |
+----+------------+---------------------+---------+
4 rows in set (0.00 sec)

mysql> SELECT id,title,created,author FROM topic WHERE author='jihyeok';
+----+--------+---------------------+---------+
| id | title  | created             | author  |
+----+--------+---------------------+---------+
|  1 | MySQL  | 2024-12-28 13:59:29 | jihyeok |
|  2 | ORACLE | 2024-12-28 14:01:26 | jihyeok |
+----+--------+---------------------+---------+
2 rows in set (0.00 sec)

mysql> SELECT id,title,created,author FROM topic WHERE author='jihyeok' ORDER BY id DESC;
+----+--------+---------------------+---------+
| id | title  | created             | author  |
+----+--------+---------------------+---------+
|  2 | ORACLE | 2024-12-28 14:01:26 | jihyeok |
|  1 | MySQL  | 2024-12-28 13:59:29 | jihyeok |
+----+--------+---------------------+---------+
2 rows in set (0.00 sec)

mysql> SELECT id,title,created,author FROM topic WHERE author='jihyeok' ORDER BY id DESC LIMIT 1;
+----+--------+---------------------+---------+
| id | title  | created             | author  |
+----+--------+---------------------+---------+
|  2 | ORACLE | 2024-12-28 14:01:26 | jihyeok |
+----+--------+---------------------+---------+
1 row in set (0.00 sec)
```

만약 데이터가 1억 건 이상이라면 `SELECT *`은 컴퓨터에 엄청난 부하를 줄 수 있다. 그래서 조건을 걸어야 한다...이런 생각을 가지고 있자.

```sql
mysql> SELECT * FROM topic;
+----+------------+--------------------------+---------------------+---------+---------------------------+
| id | title      | description              | created             | author  | profile                   |
+----+------------+--------------------------+---------------------+---------+---------------------------+
|  1 | MySQL      | MySQL is ...             | 2024-12-28 13:59:29 | jihyeok | developer                 |
|  2 | ORACLE     | ORACLE is ...            | 2024-12-28 14:01:26 | jihyeok | developer                 |
|  3 | SQL Server | SQL Server is ...        | 2024-12-28 14:02:27 | duru    | data administrator        |
|  4 | PostgreSQL | PostgreSQL Server is ... | 2024-12-28 14:03:19 | taeho   | data scientist, developer |
+----+------------+--------------------------+---------------------+---------+---------------------------+
4 rows in set (0.00 sec)

mysql> DESC topic;
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| id          | int          | NO   | PRI | NULL    | auto_increment |
| title       | varchar(100) | NO   |     | NULL    |                |
| description | text         | YES  |     | NULL    |                |
| created     | datetime     | NO   |     | NULL    |                |
| author      | varchar(30)  | YES  |     | NULL    |                |
| profile     | varchar(100) | YES  |     | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
6 rows in set (0.00 sec)

mysql> UPDATE topic SET description='Oracle is ...', title='Oracle' WHERE id=2;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM topic;
+----+------------+--------------------------+---------------------+---------+---------------------------+
| id | title      | description              | created             | author  | profile                   |
+----+------------+--------------------------+---------------------+---------+---------------------------+
|  1 | MySQL      | MySQL is ...             | 2024-12-28 13:59:29 | jihyeok | developer                 |
|  2 | Oracle     | Oracle is ...            | 2024-12-28 14:01:26 | jihyeok | developer                 |
|  3 | SQL Server | SQL Server is ...        | 2024-12-28 14:02:27 | duru    | data administrator        |
|  4 | PostgreSQL | PostgreSQL Server is ... | 2024-12-28 14:03:19 | taeho   | data scientist, developer |
+----+------------+--------------------------+---------------------+---------+---------------------------+
4 rows in set (0.00 sec)
```

데이터를 수정하는 방법이다. `WHERE` 문 특히 중요하다.

```sql
mysql> SELECT * FROM topic;
+----+------------+--------------------------+---------------------+---------+---------------------------+
| id | title      | description              | created             | author  | profile                   |
+----+------------+--------------------------+---------------------+---------+---------------------------+
|  1 | MySQL      | MySQL is ...             | 2024-12-28 13:59:29 | jihyeok | developer                 |
|  2 | Oracle     | Oracle is ...            | 2024-12-28 14:01:26 | jihyeok | developer                 |
|  3 | SQL Server | SQL Server is ...        | 2024-12-28 14:02:27 | duru    | data administrator        |
|  4 | PostgreSQL | PostgreSQL Server is ... | 2024-12-28 14:03:19 | taeho   | data scientist, developer |
+----+------------+--------------------------+---------------------+---------+---------------------------+
4 rows in set (0.00 sec)

mysql> DELETE FROM topic WHERE id=3;
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM topic;
+----+------------+--------------------------+---------------------+---------+---------------------------+
| id | title      | description              | created             | author  | profile                   |
+----+------------+--------------------------+---------------------+---------+---------------------------+
|  1 | MySQL      | MySQL is ...             | 2024-12-28 13:59:29 | jihyeok | developer                 |
|  2 | Oracle     | Oracle is ...            | 2024-12-28 14:01:26 | jihyeok | developer                 |
|  4 | PostgreSQL | PostgreSQL Server is ... | 2024-12-28 14:03:19 | taeho   | data scientist, developer |
+----+------------+--------------------------+---------------------+---------+---------------------------+
3 rows in set (0.00 sec)
```

데이터를 삭제하는 방법이다.

### - 관계형 데이터베이스의 필요성

왜 관계형 데이터베이스가 필요할까?

![image](https://github.com/user-attachments/assets/3c9a5fca-9336-480d-ac49-d99621f8b7c8)

egoing이 중복된다…

만약 저 데이터가 천만개가 넘는다고 생각해보자. 얼마나 낭비인가…

또 만약 수정해야 한다면?

만약 egoing이라는 사람이 한명이 아니라면?..

저 문제를 어떻게 해결할까?

→ 테이블을 분리한다.

![image](https://github.com/user-attachments/assets/cff69447-d042-41cf-bda6-5c0e770f4f2a)

이렇게 테이블을 분리하고 author_id로 연결한다. 아주 명확하고 이로써 동명이인이 생기더라도 헷갈리지 않는다.

그래서 만약 저자 중 “egoing”을 “이고잉”으로 수정하고 싶다면 author테이블에서만 이름을 변경하면 모든 데이터가 변경된다.

전보다 아주 효율적.

그런데 단점도 존재한다.

이렇게 두 개의 테이블로 분리시키면서 직관적이지 않다.

그러면 어떻게 하면 좋을까?

데이터를 분리하면서 중복을 제거하는 장점을 가지는데 직관적이지 않은 단점을 해결하는 방법은..?

MySQL은 그게 가능하다.

![image](https://github.com/user-attachments/assets/84da9ccd-f521-489b-91d7-26e5cf337afc)

데이터베이스는 이렇게 저장되어 있지만,

볼 때는 합쳐서 볼 수 있다. `JOIN`을 하면...

![image](https://github.com/user-attachments/assets/c1ef2f6a-aa7a-446e-8bab-d8ddfc234a3e)

저렇게 두 개의 테이블이 읽어올 때 같이 결합한 것처럼 볼 수 있다.

직관성이 높아진다.