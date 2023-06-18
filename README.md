# MS-SQL-SERVER
Find Primary key, Triggers, How many table and its name in a database.

-- TO FIND THE LATEST VERSION OF MS SQL SERVER
SELECT @@VERSION


-- HOW MANY TABLE IN A DATABASE OR ITS NAME
SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES 


SELECT TABLE_SCHEMA AS 'DATABASE' , COUNT(*) AS 'TABLES' FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_TYPE = 'BASE TABLE' GROUP BY TABLE_SCHEMA;

SELECT CURRENT_USER

-- PRIMARY KEY
SELECT COLUMN_NAME
FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE
WHERE OBJECTPROPERTY(OBJECT_ID(CONSTRAINT_SCHEMA + '.' + CONSTRAINT_NAME), 'IsPrimaryKey') = 1
AND TABLE_NAME = 'M_PDS_FARMERREG2021';

-- PRIMARY KEY
  SELECT CONSTRAINT_NAME
  FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS
  WHERE TABLE_NAME = 'PDS_VillageMaster'
  AND CONSTRAINT_TYPE = 'PRIMARY KEY'
  AND (SELECT COUNT(*) FROM INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE WHERE CONSTRAINT_NAME = CONSTRAINT_NAME) > 1;
  
  
  --TRIGGERS
  SELECT COUNT(*) AS NumberOfTriggers
FROM sys.triggers
WHERE parent_id = OBJECT_ID('M_PPAS_VR');


-- DATABASE PRINCIPAL
SELECT name as username, create_date, 
       modify_date, type_desc as type
FROM sys.database_principals
WHERE type not in ('A', 'G', 'R', 'X')
      and sid is not null
      and name != 'guest'

	  SELECT NAME AS USERNAME, CREATE_DATE,
	                MODIFY_DATE, TYPE_DESC AS TYPE
      FROM SYS.database_principals -- WHERE NOT
