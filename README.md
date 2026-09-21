# Oracle PDB Assignment II Report

## Repository Information
- Repository Link: https://github.com/IrafashCactus/oracle_pdb_ass_II_20251SEN246_irafasha
- PDB Name Created: ir_pdb_20251SEN246
- Issues Encountered: Yes

## 1. Overview of the Task
This assignment required creating a Pluggable Database (PDB), creating a user inside it, creating another temporary PDB and then deleting it, and using Oracle Enterprise Manager (OEM) for database management. The main objective was to demonstrate practical knowledge of PDB creation, user administration, and database lifecycle management in an Oracle environment.

## 2. Oracle Environment Used
- Oracle Version: Oracle AI Database 26ai Free
- Tools Used: SQL*Plus, Oracle SQL Developer
- PDB Created: ir_pdb_20251SEN246
- PDB Admin User: irafasha_plsqlauca_20251SEN246

## 3. Task Explanation

### 3.1 Task 1: Create a New Pluggable Database
The first step was to connect to the database as the super administrator using the command:

```sql
CONNECT / AS SYSDBA
```

Then I checked the current PDBs by running:

```sql
SHOW PDBS;
```

I observed the default PDBs available in the environment. Before creating the new PDB, I checked where the data files were stored because the `FILE_NAME_CONVERT` clause must point to the source seed directory and the target directory.

I executed the following queries:

```sql
SELECT name FROM v$datafile WHERE con_id = 1;
SELECT name FROM v$datafile WHERE con_id = 2;
```

After identifying the required file paths, I created the new PDB using the command below:

```sql
CREATE PLUGGABLE DATABASE ir_pdb_20251SEN246
ADMIN USER irafasha_plsqlauca_20251SEN246 IDENTIFIED BY password
ROLES = (DBA)
FILE_NAME_CONVERT = (
  'C:\APP\ATLAS\PRODUCT\26AI\ORADATA\FREE\PDBSEED\',
  'C:\APP\ATLAS\PRODUCT\26AI\ORADATA\FREE\IR_PDB_20251SEN246\'
);
```

The PDB was created successfully. I then opened it with:

```sql
ALTER PLUGGABLE DATABASE ir_pdb_20251SEN246 OPEN;
```

After that, I switched into the PDB using:

```sql
ALTER SESSION SET CONTAINER = ir_pdb_20251SEN246;
```

To confirm that the admin user was created correctly, I checked the database users using:

```sql
SELECT username, account_status FROM dba_users WHERE username = 'IRAFASHA_PLSQLAUCA_20251SEN246';
```

During this step, I initially used the username in lowercase:

```sql
SELECT username, account_status FROM dba_users WHERE username = 'irafasha_plsqlauca_20251SEN246';
```

This returned no rows because Oracle usernames are case-sensitive in this check. The correct result was obtained when the username was written in uppercase. Supporting screenshot evidence has been included in the repository as required.

### 3.2 Task 2: Create and Delete a PDB
For this task, I created another PDB using the same process as the first one. The PDB was named:

```sql
ir_to_delete_pdb_20251SEN246
```

I verified whether it existed by running:

```sql
SHOW PDBS;
```

After confirming the PDB existed, I deleted it using:

```sql
DROP PLUGGABLE DATABASE ir_to_delete_pdb_20251SEN246 INCLUDING DATAFILES;
```

This removed the PDB and its associated data files from disk. To verify that the deletion was successful, I checked the current PDB list again with:

```sql
SHOW PDBS;
```

The result was captured in the screenshots included in the repository.

### 3.3 Task 3: Oracle Enterprise Manager (OEM)
This task was challenging because I checked Oracle Enterprise Manager Express on port 5500 but found that no service was running. After further research, I discovered that Oracle Enterprise Manager Express is not included in Oracle Database 26ai Free. Because of this, I used Oracle SQL Developer as the alternative environment to manage and verify the database.

I also ran the following query to view the PDBs:

```sql
SELECT con_id, name, open_mode FROM v$pdbs ORDER BY con_id;
```

This query was executed both in SQL*Plus and Oracle SQL Developer, and both tools displayed the same result, showing three PDBs in the environment.

## 4. Challenges Faced and How They Were Solved
The main challenges encountered were:

- Typing errors during SQL commands, especially with database names and usernames.
- Case-sensitivity issues when querying `dba_users`; the username had to be written in uppercase to match Oracle's stored values.
- Oracle Enterprise Manager Express was not available in Oracle Database 26ai Free, so I used SQL Developer as a practical alternative.

These issues were resolved by carefully rechecking the commands, validating database names and user names, and using the available database tools for verification.

## 5. Integrity Statement
I confirm that all screenshots in this repository were taken from my own machine and represent my own work. I did not copy screenshots or commands from classmates, and I did not use AI tools to generate the SQL commands used in this assignment.
