CREATE TABLE FLIGHT(
     	FLIGHT_NUM INT,
     	SOURCE VARCHAR(20),
     	DESTINATION VARCHAR(20),
    	DISTANCE INT,
    	DEPARTS VARCHAR(10),
    	ARRIVES VARCHAR(10),
     	PRICE INT,
    	PRIMARY KEY (FLIGHT_NUM) );


CREATE TABLE EMPLOYEES(
     		EID INT,
    		ENAME VARCHAR(20),
    		SALARY INT,
    		PRIMARY KEY (EID) );
CREATE TABLE AIRCRAFT(
    	AID INT,
    	ANAME VARCHAR(20),
    	CRUISINGRANGE INT,
    	PRIMARY KEY (AID) );

CREATE TABLE CERTIFIED(
     		EID INT,
    		 AID INT,
    		 PRIMARY KEY (EID,AID),
     		FOREIGN KEY (EID) REFERENCES EMPLOYEES (EID),
     		FOREIGN KEY (AID) REFERENCES AIRCRAFT (AID) );


INSERT INTO FLIGHT VALUES(1,'BANGALORE','MANGALORE',300,'10:45','12:00',10000);
INSERT INTO FLIGHT VALUES(2,'BANGALORE','DELHI',5000,'12:15','4:30',25000);
INSERT INTO FLIGHT VALUES(3,'BANGALORE','MUMBAI',3500,'2:15','5:25',30000);
INSERT INTO FLIGHT VALUES(4,'DELHI','MUMBAI',4500,'10:15','12:05',35000);
INSERT INTO FLIGHT VALUES(5,'DELHI','FRANKFURT',18000,'7:15','5:30',90000);
INSERT INTO FLIGHT VALUES(6,'BANGALORE','FRANKFURT',19500,'10:00','7:45',95000);
INSERT INTO FLIGHT VALUES(7,'BANGALORE','FRANKFURT',17000,'12:00','6:30',99000);

SQL> SELECT * FROM FLIGHT;
FLIGHT_NUM SOURCE               DESTINATION            DISTANCE DEPARTS    ARRIVES         PRICE
---------- -------------------- -------------------- ---------- ---------- ---------- ----------
         1 BANGALORE            MANGALORE                   300 10:45      12:00            10000
         2 BANGALORE            DELHI                      5000 12:15      4:30             25000
         3 BANGALORE            MUMBAI                     3500 2:15       5:25             30000
         4 DELHI                MUMBAI                     4500 10:15      12:05            35000
         5 DELHI                FRANKFURT                 18000 7:15       5:30             90000
         6 BANGALORE            FRANKFURT                 19500 10:00      7:45             95000
         7 BANGALORE            FRANKFURT                 17000 12:00      6:30             99000

INSERT INTO AIRCRAFT VALUES(123,'AIRBUS',1000);
INSERT INTO AIRCRAFT VALUES(302,'BOEING',5000);
INSERT INTO AIRCRAFT VALUES(306,'JET01',5000);
INSERT INTO AIRCRAFT VALUES(378,'AIRBUS380',8000);
INSERT INTO AIRCRAFT VALUES(456,'AIRCRAFT',500);
INSERT INTO AIRCRAFT VALUES(789,'AIRCRAFT02',800);
INSERT INTO AIRCRAFT VALUES(951,'AIRCRAFT03',1000);

SQL> SELECT * FROM AIRCRAFT;

       AID ANAME                CRUISINGRANGE
---------- -------------------- -------------
       123 AIRBUS                        1000
       302 BOEING                        5000
       306 JET01                         5000
       378 AIRBUS380                     8000
       456 AIRCRAFT                       500
       789 AIRCRAFT02                     800
       951 AIRCRAFT03                    1000

INSERT INTO EMPLOYEES VALUES(1,'AJAY',30000);
INSERT INTO EMPLOYEES VALUES(2,'AJITH',85000);
INSERT INTO EMPLOYEES VALUES(3,'ARNAB',50000);
INSERT INTO EMPLOYEES VALUES(4,'HARRY',45000);
INSERT INTO EMPLOYEES VALUES(5,'ARUN',90000);
INSERT INTO EMPLOYEES VALUES(6,'JOSH',75000);
INSERT INTO EMPLOYEES VALUES(7,'RAM',100000);
SQL> SELECT * FROM EMPLOYEES;

       EID ENAME                    SALARY
---------- -------------------- ----------
         1 AJAY                      30000
         2 AJITH                     85000
         3 ARNAB                     50000
         4 HARRY                     45000
         5 ARUN                      90000
         6 JOSH                      75000
         7 RAM                      100000

INSERT INTO CERTIFIED VALUES(1,123);
INSERT INTO CERTIFIED VALUES(2,123);
INSERT INTO CERTIFIED VALUES(1,302);
INSERT INTO CERTIFIED VALUES(5,302);
INSERT INTO CERTIFIED VALUES(7,302);
INSERT INTO CERTIFIED VALUES(1,306);
INSERT INTO CERTIFIED VALUES(2,306);
INSERT INTO CERTIFIED VALUES(1,378);
INSERT INTO CERTIFIED VALUES(2,378);
INSERT INTO CERTIFIED VALUES(4,378);
INSERT INTO CERTIFIED VALUES(3,456);
INSERT INTO CERTIFIED VALUES(6,456);
INSERT INTO CERTIFIED VALUES(1,789);
INSERT INTO CERTIFIED VALUES(5,789);
INSERT INTO CERTIFIED VALUES(6,789);
INSERT INTO CERTIFIED VALUES(1,951);
INSERT INTO CERTIFIED VALUES(3,951);


SQL> SELECT * FROM CERTIFIED;

       EID        AID
---------- ----------
         1        123
         1        302
         1        306
         1        378
         1        789
         1        951
         2        123
         2        306
         2        378
         3        456
         3        951
         4        378
         5        302
         5        789
         6        456
         6        789
         7        302
      
QUERY 1:
SQL> SELECT DISTINCT a.aname
  2       FROM aircraft a, certified c, employees e
  3       WHERE a.aid=c.aid
  4       AND c.eid=e.eid
  5       AND NOT EXISTS
  6      (SELECT *
  7      FROM employees e1
  8       WHERE e1.eid=e.eid
  9       AND e1.salary<80000);
ANAME
--------------------
AIRBUS
AIRCRAFT02
BOEING
JET01
AIRBUS380
QUERY 2:
SQL> SELECT c.eid,MAX(cruisingrange)
  2       FROM certified c,aircraft a
  3       WHERE c.aid=a.aid
  4      GROUP BY c.eid
  5      HAVING COUNT(*)>3;

       EID MAX(CRUISINGRANGE)
---------- ------------------
         1               8000
QUERY 3:
SQL> SELECT DISTINCT e.ename
      FROM employees e
      WHERE e.salary<=
      (SELECT MIN(f.price)
      FROM flight f
      WHERE f.Source='BANGALORE'
       AND f.Destination='MUMBAI');
ENAME
--------------------
AJAY

QUERY 4:
SQL> SELECT a.aid
     FROM aircraft a
     WHERE a.cruisingrange>
     (SELECT MIN(f.distance)
     FROM flight f
     WHERE f.Source='BANGALORE'
     AND f.Destination='DELHI');

      AID
---------
      378

query 5:

SELECT ename,salary from employees where salary=(select MAX(salary) 
FROM employees 
WHERE salary <(select max(salary)from employees));

ENAME                    SALARY
-------------------- ----------
ARUN                      90000
