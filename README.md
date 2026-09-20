 Repository Link: https://github.com/IrafashCactus/oracle_pdb_ass_II_20251SEN246_irafasha
 PDB Name Created: ir_pdb_20251SEN246
 Issues Encountered: Yes



1. OVERVIEW OF TASK 
this assignment were  asking to create pluggable databases (pdb), creating user in it ,  creating and temporary another pdb and deleting it, and also to use oracle enterprise management.

  2. Oracle Environment Used
  Oracle Version :oracle AI Database 26ai free
  Tools used :SQL*Plus, Oracle sql developer
  PDB created : ir_pdb_20251SEN246
  PDB Admin User:irafasha_plsqlauca_20251SEN246

  3. Task Explanation
  Task 1: Create a New Pluggable Database
  first of all i ented /connect to database  as super admin by / as sysdba command and check CURRENT PDB BY SHOW PDBS; COMMAND. You will see two default pdb i saw in screenshot before i create PDB i checked where the datafiles are stored, because the FILE_NAME_CONVERT clause requires me to know the source (seed) path and 
  the target path i run SELECT name FROM v$datafile WHERE con_id = 1; and SELECT name FROM v$datafile WHERE con_id = 2;  after getting them i created PDB with   CREATE PLUGGABLE DATABASE ir_pdb_20251SEN246
      ADMIN USER irafasha_plsqlauca_20251SEN246 IDENTIFIED BY password
      ROLES = (DBA)
      FILE_NAME_CONVERT = (
        'C:\APP\ATLAS\PRODUCT\26AI\ORADATA\FREE\PDBSEED\',
        'C:\APP\ATLAS\PRODUCT\26AI\ORADATA\FREE\IR_PDB_20251SEN246\'
      ); 
 PDB was created successfully i opened it with 
 ALTER PLUGGABLE DATABASE ir_pdb_20251SEN246 OPEN;  then i switched into it  by running 
 ALTER SESSION SET CONTAINER = ir_pdb_20251SEN246;
 after getting inside i checked user by running 
 SELECT username, account_status FROM dba_users WHERE username = 'IRAFASHA_PLSQLAUCA_20251SEN246'; but here i firts used condition WHERE username = 'irafasha_plsqlauca_20251SEN246'; IN SMALL LETTER AND GIVES NO ROWS SELECTED  means you have to use capital letter
 and there are supportive screenshot  evidence  as required 

   Task 2: Create and Delete a PDB
   on this task i created PDB follow the some step as created first one here used name of ir_to_delete_pdb_20251SEN246 and checked if exist by running SHOW PDBS;
   After seen that it exist i dropped it by running 
   DROP PLUGGABLE DATABASE ir_to_delete_pdb_20251SEN246 INCLUDING DATAFILES; to remove PDB and its files from disk  to confirm if its deleted successful i also verfy bt running SHOW PDBS;
    you will them on screenshot

 Task 3: Oracle Enterprise Manager (OEM)
  this task is one which disappointed me i checked port 5500 for oracle enterprise management express but i found no service running  After research i found that  OEM express is not included in oracle database 26ai Free and i used SQL developer as alternative  i run SELECT con_id, name, open_mode FROM v$pdbs ORDER BY con_id; but i also runned it in SQL*Plus  both they displayed 3 PDBS.

4. Challenges Faced and How They Were Solved
my challenge many of them are about typing error and OEM express which is not available 

5. Integrity Statement
I confirm that all screenshot in this repository are my own work executed on my machine. i did not copy from classmates and i did not use AI tool to generate commands. 