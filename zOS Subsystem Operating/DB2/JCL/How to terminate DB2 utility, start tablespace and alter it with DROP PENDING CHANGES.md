# Terminate DB2 Utility. Start DB2 Tablespace with RW access. Alter DB2 Tablespace with DROP PENDING CHANGES

```
//******************************************************//
//*  INSTRUCTIONS:                                     *//
//*  1. REPLACE DB2_SDSNLOAD WITH YOUR SDSNLOAD DS     *//
//*  2. REPLACE SUBSYSTEM_NAME WITH YOUR DB2 SUBSYSTEM *//
//*     NAME                                           *//
//*  3. REPLACE UTID WITH YOUR DB2 UTILITY ID          *//
//*  4. REPLACE DATABASE_NAME WITH YOUR DATABASE NAME  *//
//*  5. REPLACE TABLESPACE_NAME WITH YOUR TABLESPACE   *//
//*     NAME                                           *//
//*  6. REPLACE DB2_RUNLIB_LOAD WITH YOUR RUNLIB LOAD DS//
//*
//START1    EXEC PGM=IKJEFT01,DYNAMNBR=20
//SYSTSPRT  DD SYSOUT=*
//STEPLIB   DD DSN=DB2_SDSNLOAD,DISP=SHR
//SYSPRINT  DD SYSOUT=*
//SYSUDUMP  DD SYSOUT=*
//SYSOUT    DD SYSOUT=*
//SYSTSIN   DD *
  DSN SYSTEM(SUBSYSTEM_NAME)
  -TERM UTIL (UTID)
  -STA DB(DATABASE_NAME) SPACENAM(TABLESPACE_NAME) ACCESS(RW)
  END
//SYSIN     DD DUMMY
//ALTER1    EXEC PGM=IKJEFT01
//STEPLIB   DD  DSN=DB2_SDSNLOAD,
//             DISP=SHR
//SYSTSIN   DD  *
  DSN SYSTEM(SUBSYSTEM_NAME)
  RUN PROGRAM(DSNTEP2) PLAN(DSNTEP11)  -
  LIB('DB2_RUNLIB_LOAD')
  END
//*
//SYSIN     DD  *
  ALTER TABLESPACE DATABASE_NAME.TABLESPACE_NAME DROP PENDING CHANGES;
/*
//SYSTSPRT  DD  SYSOUT=*
//SYSPRINT  DD  SYSOUT=*  
```