Q1. Create table patients:
mysql> select * from patients;
+------+----------------+------+--------+--------------------+------------+------------+-----------+
| p_id | p_name         | age  | gender | date_of_admisssion | status     | city       | doctor_id |
+------+----------------+------+--------+--------------------+------------+------------+-----------+
|    1 | Archana rane   |   35 | Female | 2024-01-02         | Discharged | Mumbai     |         3 |
|    2 | Rupali Mhatre  |   40 | Female | 2023-12-02         | Admitted   | Pune       |         4 |
|    6 | Sanket ujgare  |   25 | Male   | 2021-01-02         | Admitted   | Pune       |         1 |
|    7 | rakesh Man     |   28 | Male   | 2022-01-03         | Discharged | Nagpur     |         2 |
|    8 | Suyash rane    |   30 | Male   | 2023-04-05         | Admitted   | Pune       |         3 |
|    9 | Kalpana rathi  |   29 | Female | 2024-01-01         | Discharged | Ahamedabad |         5 |
|   10 | mayur tripathi |   29 | Male   | 2022-04-07         | Admitted   | Ranchi     |         4 |
+------+----------------+------+--------+--------------------+------------+------------+-----------+
7 rows in set (0.00 sec)

Q2. create table doctor:
mysql> select * from doctor;
+-----------+------+--------+------------+----------------+---------------------+--------+--------------------+
| doctor_id | age  | gender | city       | specialization | years_of_experience | salary | name               |
+-----------+------+--------+------------+----------------+---------------------+--------+--------------------+
|         1 |   34 | Male   | Ahamedabad | MD-Surgan      |                  12 |  50000 | Aman Gupta         |
|         2 |   38 | Male   | Pune       | MD-ortho       |                  13 |  60000 | rakesh Junjhunwala |
|         3 |   40 | Male   | Ahamedabad | MD-Heart       |                  12 |  45000 | Akash Thosar       |
|         4 |   28 | Female | Nagpur     | MD-Nervous     |                  10 |  55000 | Rupali Mane        |
|         5 |   30 | Female | Pune       | MD-Cervical    |                   5 |  50000 | Sanjana Gupta      |
+-----------+------+--------+------------+----------------+---------------------+--------+--------------------+
5 rows in set (0.00 sec)

Q3.alter coloumn specialization to subject:
mysql> alter table doctor rename column specialization to subject;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc doctor;
+---------------------+-------------+------+-----+---------+----------------+
| Field               | Type        | Null | Key | Default | Extra          |
+---------------------+-------------+------+-----+---------+----------------+
| doctor_id           | int         | NO   | PRI | NULL    | auto_increment |
| age                 | int         | YES  |     | NULL    |                |
| gender              | varchar(25) | YES  |     | NULL    |                |
| city                | varchar(25) | YES  |     | NULL    |                |
| subject             | varchar(25) | YES  |     | NULL    |                |
| years_of_experience | int         | YES  |     | NULL    |                |
| salary              | int         | YES  |     | NULL    |                |
| name                | varchar(25) | YES  |     | NULL    |                |
+---------------------+-------------+------+-----+---------+----------------+
8 rows in set (0.01 sec)

Q4.create backup table 
mysql> create table bkup_patient like patients;
Query OK, 0 rows affected (0.06 sec)

mysql> create table bkup_doctor like doctor;
Query OK, 0 rows affected (0.04 sec)

mysql> desc bkup_patients;
ERROR 1146 (42S02): Table 'eltp_batch1.bkup_patients' doesn't exist
mysql> desc bkup_patient;
+--------------------+-------------+------+-----+---------+----------------+
| Field              | Type        | Null | Key | Default | Extra          |
+--------------------+-------------+------+-----+---------+----------------+
| p_id               | int         | NO   | PRI | NULL    | auto_increment |
| p_name             | varchar(25) | YES  |     | NULL    |                |
| age                | int         | YES  |     | NULL    |                |
| gender             | varchar(10) | YES  |     | NULL    |                |
| date_of_admisssion | date        | YES  |     | NULL    |                |
| status             | varchar(25) | YES  |     | NULL    |                |
| city               | varchar(25) | YES  |     | NULL    |                |
| doctor_id          | int         | YES  | MUL | NULL    |                |
+--------------------+-------------+------+-----+---------+----------------+
8 rows in set (0.01 sec)

mysql> desc bkup_doctor;
+---------------------+-------------+------+-----+---------+----------------+
| Field               | Type        | Null | Key | Default | Extra          |
+---------------------+-------------+------+-----+---------+----------------+
| doctor_id           | int         | NO   | PRI | NULL    | auto_increment |
| age                 | int         | YES  |     | NULL    |                |
| gender              | varchar(25) | YES  |     | NULL    |                |
| city                | varchar(25) | YES  |     | NULL    |                |
| subject             | varchar(25) | YES  |     | NULL    |                |
| years_of_experience | int         | YES  |     | NULL    |                |
| salary              | int         | YES  |     | NULL    |                |
| name                | varchar(25) | YES  |     | NULL    |                |
+---------------------+-------------+------+-----+---------+----------------+
8 rows in set (0.01 sec)

mysql> insert into bkup_patient select * from patients;
Query OK, 7 rows affected (0.01 sec)
Records: 7  Duplicates: 0  Warnings: 0

mysql> insert into bkup_doctor select * from doctor;
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> select * from bkup_patients;
ERROR 1146 (42S02): Table 'eltp_batch1.bkup_patients' doesn't exist
mysql> select * from bkup_patient;
+------+----------------+------+--------+--------------------+------------+------------+-----------+
| p_id | p_name         | age  | gender | date_of_admisssion | status     | city       | doctor_id |
+------+----------------+------+--------+--------------------+------------+------------+-----------+
|    1 | Archana rane   |   35 | Female | 2024-01-02         | Discharged | Mumbai     |         3 |
|    2 | Rupali Mhatre  |   40 | Female | 2023-12-02         | Admitted   | Pune       |         4 |
|    6 | Sanket ujgare  |   25 | Male   | 2021-01-02         | Admitted   | Pune       |         1 |
|    7 | rakesh Man     |   28 | Male   | 2022-01-03         | Discharged | Nagpur     |         2 |
|    8 | Suyash rane    |   30 | Male   | 2023-04-05         | Admitted   | Pune       |         3 |
|    9 | Kalpana rathi  |   29 | Female | 2024-01-01         | Discharged | Ahamedabad |         5 |
|   10 | mayur tripathi |   29 | Male   | 2022-04-07         | Admitted   | Ranchi     |         4 |
+------+----------------+------+--------+--------------------+------------+------------+-----------+
7 rows in set (0.00 sec)

mysql> select * from bkup_doctor;
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
| doctor_id | age  | gender | city       | subject     | years_of_experience | salary | name               |
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
|         1 |   34 | Male   | Ahamedabad | MD-Surgan   |                  12 |  51000 | Aman Gupta         |
|         2 |   38 | Male   | Pune       | MD-ortho    |                  13 |  61000 | rakesh Junjhunwala |
|         3 |   40 | Male   | Ahamedabad | MD-Heart    |                  12 |  46000 | Akash Thosar       |
|         4 |   28 | Female | Nagpur     | MD-Nervous  |                  10 |  56000 | Rupali Mane        |
|         5 |   30 | Female | Pune       | MD-Cervical |                   5 |  51000 | Sanjana Gupta      |
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
5 rows in set (0.00 sec)

Q5.find all patients from pune and mumbai;
mysql> select * from patients where city='Pune' or city='Mumbai';
+------+---------------+------+--------+--------------------+------------+--------+-----------+
| p_id | p_name        | age  | gender | date_of_admisssion | status     | city   | doctor_id |
+------+---------------+------+--------+--------------------+------------+--------+-----------+
|    1 | Archana rane  |   35 | Female | 2024-01-02         | Discharged | Mumbai |         3 |
|    2 | Rupali Mhatre |   40 | Female | 2023-12-02         | Admitted   | Pune   |         4 |
|    6 | Sanket ujgare |   25 | Male   | 2021-01-02         | Admitted   | Pune   |         1 |
|    8 | Suyash rane   |   30 | Male   | 2023-04-05         | Admitted   | Pune   |         3 |
+------+---------------+------+--------+--------------------+------------+--------+-----------+
4 rows in set (0.00 sec)


Q6: find all doctors from ahamedabad starts with A:
mysql> select * from doctor where city='Ahamedabad' and name like 'A%';
+-----------+------+--------+------------+-----------+---------------------+--------+--------------+
| doctor_id | age  | gender | city       | subject   | years_of_experience | salary | name         |
+-----------+------+--------+------------+-----------+---------------------+--------+--------------+
|         1 |   34 | Male   | Ahamedabad | MD-Surgan |                  12 |  50000 | Aman Gupta   |
|         3 |   40 | Male   | Ahamedabad | MD-Heart  |                  12 |  45000 | Akash Thosar |
+-----------+------+--------+------------+-----------+---------------------+--------+--------------+
2 rows in set (0.00 sec)

Q7:find doctors having 4 or more than 4 years of experience:
sle
mysql> select * from doctor where years_of_experience>=4 and doctor_id in(select doctor_id from patients);
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
| doctor_id | age  | gender | city       | subject     | years_of_experience | salary | name               |
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
|         1 |   34 | Male   | Ahamedabad | MD-Surgan   |                  12 |  50000 | Aman Gupta         |
|         2 |   38 | Male   | Pune       | MD-ortho    |                  13 |  60000 | rakesh Junjhunwala |
|         3 |   40 | Male   | Ahamedabad | MD-Heart    |                  12 |  45000 | Akash Thosar       |
|         4 |   28 | Female | Nagpur     | MD-Nervous  |                  10 |  55000 | Rupali Mane        |
|         5 |   30 | Female | Pune       | MD-Cervical |                   5 |  50000 | Sanjana Gupta      |
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
5 rows in set (0.00 sec)

Q8:increase salary of all doctors by 1000 having more than 5 years of experience:
mysql> select * from doctor;
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
| doctor_id | age  | gender | city       | subject     | years_of_experience | salary | name               |
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
|         1 |   34 | Male   | Ahamedabad | MD-Surgan   |                  12 |  51000 | Aman Gupta         |
|         2 |   38 | Male   | Pune       | MD-ortho    |                  13 |  61000 | rakesh Junjhunwala |
|         3 |   40 | Male   | Ahamedabad | MD-Heart    |                  12 |  46000 | Akash Thosar       |
|         4 |   28 | Female | Nagpur     | MD-Nervous  |                  10 |  56000 | Rupali Mane        |
|         5 |   30 | Female | Pune       | MD-Cervical |                   5 |  51000 | Sanjana Gupta      |
+-----------+------+--------+------------+-------------+---------------------+--------+--------------------+
5 rows in set (0.00 sec)

Q9:find number of patients as per city:
mysql> select city, count(p_id) from patients group by city;
+------------+-------------+
| city       | count(p_id) |
+------------+-------------+
| Mumbai     |           1 |
| Pune       |           3 |
| Nagpur     |           1 |
| Ahamedabad |           1 |
| Ranchi     |           1 |
+------------+-------------+
5 rows in set (0.00 sec)

Q10:retrive patient record having 3 or more exp
mysql> select * from patients where status='Discharged' and doctor_id in (select doctor_id from doctor where years_of_experience>=3);
+------+---------------+------+--------+--------------------+------------+------------+-----------+
| p_id | p_name        | age  | gender | date_of_admisssion | status     | city       | doctor_id |
+------+---------------+------+--------+--------------------+------------+------------+-----------+
|    1 | Archana rane  |   35 | Female | 2024-01-02         | Discharged | Mumbai     |         3 |
|    7 | rakesh Man    |   28 | Male   | 2022-01-03         | Discharged | Nagpur     |         2 |
|    9 | Kalpana rathi |   29 | Female | 2024-01-01         | Discharged | Ahamedabad |         5 |
+------+---------------+------+--------+--------------------+------------+------------+-----------+
3 rows in set (0.00 sec)

Q11:craete backup table without coping data
mysql> create table backup_patients like patients;
Query OK, 0 rows affected (0.06 sec)

mysql> select * from backup_patients;
Empty set (0.01 sec)

Q12.
mysql> select * from store;
+----------+-----------------------------------------+
| image_id | image_path                              |
+----------+-----------------------------------------+
|        1 | C:UsersCoditas-AdminPicturesScreenshots |
+----------+-----------------------------------------+
1 row in set (0.00 sec)
