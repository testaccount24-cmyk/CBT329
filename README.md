# CBT329
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 329 IS FROM TOM BRENNAN OF SOUTHERN CALIFORNIA EDISON     *   FILE 329
//*           IN ROSEMEAD, CALIFORNIA, AND CONTAINS THEIR JES2      *   FILE 329
//*           CONVERTER EXIT, EXIT 6.  IT IS A GOOD CODING EXAMPLE  *   FILE 329
//*           FOR TEACHING THE CAPABILITIES OF JES2 EXIT 6.         *   FILE 329
//*                                                                 *   FILE 329
//*     TOM BRENNAN                                                 *   FILE 329
//*     SOUTHERN CALIFORNIA EDISON CO.                              *   FILE 329
//*     2255 WALNUT GROVE AVE.                                      *   FILE 329
//*     ROSEMEAD, CA   91770                                        *   FILE 329
//*     626-302-7212                                                *   FILE 329
//*     BRENNATG@SCE.COM  OR  TOMBRENNAN@EARTHLINK.NET              *   FILE 329
//*                                                                 *   FILE 329
//*     ======================================================      *   FILE 329
//*                                                                 *   FILE 329
//*     APRIL 24, 1998                                              *   FILE 329
//*                                                                 *   FILE 329
//*     THIS DOC DESCRIBES THE JES2 EXIT 6 (CONVERTER EXIT) IN      *   FILE 329
//*     USE AT SOUTHERN CALIFORNIA EDISON CO.  ORIGINALLY           *   FILE 329
//*     OBTAINED BEFORE MY TIME FROM JOHN V. HOOPER AT              *   FILE 329
//*     NORTHWESTERN BANK, IT'S BEEN MODIFIED HEAVILY OVER THE      *   FILE 329
//*     YEARS TO DO THE THINGS WE'VE NEEDED.                        *   FILE 329
//*                                                                 *   FILE 329
//*     PLEASE REMEMBER THAT THE CODE IS SPECIFICALLY TAILORED      *   FILE 329
//*     TO OUR ENVIRONMENT, AND WOULD NEVER WORK AS-IS FOR          *   FILE 329
//*     ANYONE ELSE.  STILL, IT MAY PROVIDE CHUNKS OF CODE          *   FILE 329
//*     SOMEONE MAY WANT TO COPY AND MODIFY FOR THEIR OWN USE.      *   FILE 329
//*                                                                 *   FILE 329
//*     ALSO REMEMBER THAT THIS CODE WAS MODIFIED UNDER             *   FILE 329
//*     PRESSURE, AS I ASSUME ALL PRODUCTION CODE IS.  I DID        *   FILE 329
//*     MOST OF THE MODS MYSELF OVER MANY YEARS, AND WAS HAPPY      *   FILE 329
//*     ENOUGH WHEN THE CODE WORKED - NOT CARING TOO MUCH HOW       *   FILE 329
//*     ELEGANT, CONCISE, OR EFFICIENT THE CODE MIGHT BE.  I'M      *   FILE 329
//*     CERTAINLY NOT A JES2 OR ASSEMBLER EXPERT, BUT WHEN          *   FILE 329
//*     SOMETHING WORKS, WHAT CAN YOU SAY? :)                       *   FILE 329
//*                                                                 *   FILE 329
//*     GOOD LUCK!                                                  *   FILE 329
//*     TOM BRENNAN                                                 *   FILE 329
//*                                                                 *   FILE 329
//*     OR YELL AT ME IN THE BIT.LISTSERV.IBM-MAIN NEWSGROUP -      *   FILE 329
//*     A GREAT PLACE FOR PEOPLE LIKE ME TO LISTEN TO THE REAL      *   FILE 329
//*     EXPERTS.                                                    *   FILE 329
//*                                                                 *   FILE 329
//*     =======================================================     *   FILE 329
//*                                                                 *   FILE 329
//*     WHAT DOES OUR EXIT 6 DO FOR US?                             *   FILE 329
//*     -------------------------------                             *   FILE 329
//*                                                                 *   FILE 329
//*       O  SELECTS AN APPROPRIATE JOB CLASS, BASED ON THE         *   FILE 329
//*          FOLLOWING ITEMS:                                       *   FILE 329
//*                                                                 *   FILE 329
//*           -  THE DATAGROUP NAME PASSED TO US BY EXIT 4          *   FILE 329
//*           -  THE ORIGINAL CLASS= CARD (SOME CLASSES ARE NOT     *   FILE 329
//*              ALTERED)                                           *   FILE 329
//*           -  THE NUMBER OF TAPES USED IN THE JOB                *   FILE 329
//*           -  THE ESTIMATED CPU TIME THE JOB WILL USE            *   FILE 329
//*           -  OTHER STUFF - I FORGOT!                            *   FILE 329
//*                                                                 *   FILE 329
//*       O  ENFORCES A FEW JCL STANDARDS, SUCH AS:                 *   FILE 329
//*                                                                 *   FILE 329
//*           -  ACCOUNTING INFORMATION                             *   FILE 329
//*                                                                 *   FILE 329
//*       O  LIMITS (BY RACF) ABILITY TO USE CERTAIN JCL ITEMS:     *   FILE 329
//*                                                                 *   FILE 329
//*           -  PRODUCTION DATAGROUP NAMES                         *   FILE 329
//*           -  PRODUCTION JOB AND SYSOUT CLASSES                  *   FILE 329
//*           -  TIME=1440                                          *   FILE 329
//*           -  TAPE RETENTION OVER 120 DAYS                       *   FILE 329
//*           -  PROGRAMS SUCH AS AMASPZAP (LEFTOVER FROM LONG      *   FILE 329
//*              AGO)                                               *   FILE 329
//*           -  TAPE ROBOT USAGE (THE SILOS)                       *   FILE 329
//*           -  JOBCAT AND STEPCAT                                 *   FILE 329
//*                                                                 *   FILE 329
//*       O  CREATES /*SETUP MESSAGES FOR EACH TAPE THAT IS NOT     *   FILE 329
//*          ALREADY IN THE SILO.                                   *   FILE 329
//*                                                                 *   FILE 329
//*       O  DISPLAYS A SUMMARY OF JOB STEPS, INCLUDING:            *   FILE 329
//*                                                                 *   FILE 329
//*           - STEP AND PROC NAME                                  *   FILE 329
//*           - NUMBER OF TAPES USED BY THIS STEP                   *   FILE 329
//*           - ESTIMATED TIME FOR THIS STEP                        *   FILE 329
//*           - REGION SIZE FOR THIS STEP                           *   FILE 329
//*                                                                 *   FILE 329
//*       O  FOR TSO AND STC'S, THIS EXIT CALLS A ROUTINE TO        *   FILE 329
//*          GATHER THE ROOM NUMBER, PROGRAMMER NAME, AND           *   FILE 329
//*          ACCOUNTING STRING, AND MOVE THEM INTO THE JCT.         *   FILE 329
//*          ALSO ADDS THE DATAGROUP NAME AS THE 10TH ACCOUNTING    *   FILE 329
//*          FIELD, SO IT'S AVAILABLE IN THE ACT FOR LATER USE      *   FILE 329
//*          BY ANY PROGRAM.                                        *   FILE 329
//*                                                                 *   FILE 329
//*       O  CHECKED EACH NON-NEW DATASET NAME IN THE JOB TO        *   FILE 329
//*          MAKE SURE THAT THE CATALOG FOR THE                     *   FILE 329
//*          HIGH-LEVEL-INDEX WAS ONLINE TO THE SYSTEM              *   FILE 329
//*          CONVERTING THE JOB.  WITH OUR UNUSUAL (ABNORMAL?)      *   FILE 329
//*          IDEA OF DUMMY ALIASES ON ALL SYSTEMS, THIS HELPED      *   FILE 329
//*          ELIMINATE A LOT OF CATALOG DASD MOUNT REQUESTS         *   FILE 329
//*          WHEN A USER TYPED A HIGH-LEVEL BELONGING TO            *   FILE 329
//*          ANOTHER SYSTEM.                                        *   FILE 329
//*                                                                 *   FILE 329
//*       O  THE EXIT ALSO (UNFORTUNATELY) MUST CHECK SIMPLE        *   FILE 329
//*          ITEMS LIKE THE LENGTH OF STEP NAMES AND DATASET        *   FILE 329
//*          NAMES, BECAUSE IT NEEDS TO PUT THESE ITEMS IN A        *   FILE 329
//*          TABLE.  ERRORS IN THESE LENGTHS RESULT IN ERRORS       *   FILE 329
//*          FROM EXIT 6, WHICH CAN BE CONFUSING TO USERS WHO       *   FILE 329
//*          NORMALLY GET A REAL JES2 ERROR MESSAGE FOR THOSE       *   FILE 329
//*          MISTAKES.                                              *   FILE 329
//*                                                                 *   FILE 329
```
