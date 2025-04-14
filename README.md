# CBT1051
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE1051 is from Ben Marino and contains his Dynamic SMF       *   FILE1051
//*           Exits altering facility called zEMF.                  *   FILE1051
//*                                                                 *   FILE1051
//*           This is a marvelous package.  (SBG)                   *   FILE1051
//*                                                                 *   FILE1051
//*     >>>>  THIS PACKAGE DYNAMICALLY ALTERS YOUR SMF EXITS. <<<<  *   FILE1051
//*                  (It operates as a z/OS subsystem)              *   FILE1051
//*                                                                 *   FILE1051
//*      PURPOSE OF THE zEMF PACKAGE:                               *   FILE1051
//*                                                                 *   FILE1051
//*      zEMF does not change the settings of the SMFPRMxx          *   FILE1051
//*      PARMLIB member. SMF already has this support to alter      *   FILE1051
//*      those parameters thru the SETSMF system command, which     *   FILE1051
//*      acts by changing which SMFPRMxx PARMLIB member is now      *   FILE1051
//*      active.                                                    *   FILE1051
//*                                                                 *   FILE1051
//*      BUT WE WANT TO ADJUST THE SMF SETTINGS WITHOUT             *   FILE1051
//*      DOING EITHER OF THE FOLLOWING:                             *   FILE1051
//*                                                                 *   FILE1051
//*      1.  Changing the SMFPRMxx PARMLIB member in any            *   FILE1051
//*          way.                                                   *   FILE1051
//*                                                                 *   FILE1051
//*      2.  Changing the IBM-distributed SMF exits in any way.     *   FILE1051
//*                                                                 *   FILE1051
//*      The reason for zEMF is to allow you to extend the          *   FILE1051
//*      functionality of the SMF exits distributed by MVS          *   FILE1051
//*      without changing a single line of code.  zEMF makes SMF    *   FILE1051
//*      modifications dynamically thru sets of parameters          *   FILE1051
//*      specifically designed for each exit.                       *   FILE1051
//*                                                                 *   FILE1051
//*      You just have to learn how to use the parameters built     *   FILE1051
//*      into zEMF, to change the attributes and control which      *   FILE1051
//*      each SMF exit accomplishes.                                *   FILE1051
//*                                                                 *   FILE1051
//*      -------------------------------------------------------    *   FILE1051
//*                                                                 *   FILE1051
//*      Please look at member $$NOTE01 first.                      *   FILE1051
//*                                                                 *   FILE1051
//*      email:  Ben Marino <b2marino@outlook.com>                  *   FILE1051
//*                                                                 *   FILE1051
//*                             zEMF                                *   FILE1051
//*              DYNAMIC SMF EXITS ALTERATION FACILITY              *   FILE1051
//*                          DESCRIPTION                            *   FILE1051
//*                                                                 *   FILE1051
//*    DYNAMIC SMF EXITS ALTERATION FACILITY:                       *   FILE1051
//*                                                                 *   FILE1051
//*    Bid farewell to the hassle of modifying source code every    *   FILE1051
//*    time you want to add or alter SMF exits.                     *   FILE1051
//*                                                                 *   FILE1051
//*    Introducing zEMF, an automation tool that enables dynamic    *   FILE1051
//*    addition or modification of SMF exits.                       *   FILE1051
//*                                                                 *   FILE1051
//*    Define your SMF exits rules effortlessly in the zEMF         *   FILE1051
//*    PARMLIB, and you're good to go.                              *   FILE1051
//*                                                                 *   FILE1051
//*    Check out the example below for the rules outlined in the    *   FILE1051
//*    zEMF PARMLIB member, IEFUTL:                                 *   FILE1051
//*                                                                 *   FILE1051
//*    ---------------------------------------------------------    *   FILE1051
//*                                                                 *   FILE1051
//*    The following is a description of why Systems                *   FILE1051
//*    Programmers need zEMF.                                       *   FILE1051
//*                                                                 *   FILE1051
//*     zEMF Dynamic SMF Exits Alteration Facility:                 *   FILE1051
//*                                                                 *   FILE1051
//*     The MVS operating system's SMF component is equipped with   *   FILE1051
//*     various default SMF exits that activate when resource       *   FILE1051
//*     limits are exceeded, necessitating intervention.  These     *   FILE1051
//*     exits oversee maximum CPU and SYSOUT limits, determine      *   FILE1051
//*     which SMF records are to be written or omitted from the     *   FILE1051
//*     active SMF dataset, manage dumping when the dataset         *   FILE1051
//*     reaches capacity, and handle the switch between SMF         *   FILE1051
//*     recording datasets.                                         *   FILE1051
//*                                                                 *   FILE1051
//*     One such default exit, the IEFUTL SMF exit, functions as    *   FILE1051
//*     follows:  It is triggered when the JOB, STEP, or JOB        *   FILE1051
//*     WAIT time limit expires.  If the JOB's CPU time limit       *   FILE1051
//*     expires, the exit terminates the JOB.  If the STEP's CPU    *   FILE1051
//*     time limit expires, it extends the limit by a fixed         *   FILE1051
//*     amount.  Similarly, if the continuous WAIT time limit       *   FILE1051
//*     expires, it extends the wait time.  However, if more        *   FILE1051
//*     than three extensions are needed, the JOB is terminated.    *   FILE1051
//*     This default exit applies uniformly to all workloads        *   FILE1051
//*     running on the system, regardless of whether they are       *   FILE1051
//*     JOBs, Started Tasks, or TSO sessions.                       *   FILE1051
//*                                                                 *   FILE1051
//*     zEMF allows you to make the action of the IEFUTL SMF        *   FILE1051
//*     exit more granular.  zEMF can allow the IEFUTL exit         *   FILE1051
//*     to treat different types of system tasks differently.       *   FILE1051
//*                                                                 *   FILE1051
//*     Customizing the behavior of an SMF exit requires Systems    *   FILE1051
//*     Programmers to code the necessary changes, conduct          *   FILE1051
//*     thorough testing, and implement the modified exits into     *   FILE1051
//*     the MVS operating system, necessitating an IPL to take      *   FILE1051
//*     effect.  Any bugs during SMF exit execution can             *   FILE1051
//*     jeopardize the workload's integrity and even lead to        *   FILE1051
//*     system crashes.                                             *   FILE1051
//*                                                                 *   FILE1051
//*     The zEMF Exits Management Subsystem Server, addresses       *   FILE1051
//*     these challenges by allowing System Programmers to          *   FILE1051
//*     implement changes to SMF exits without altering the         *   FILE1051
//*     code.  zEMF enables quick modification and dynamic          *   FILE1051
//*     implementation of rules into the MVS operating system       *   FILE1051
//*     simply by defining external SMF exit rules. This            *   FILE1051
//*     eliminates potential risks to production workload           *   FILE1051
//*     activity and eliminates the need for MVS operating          *   FILE1051
//*     system IPLs when implementing SMF exit changes.             *   FILE1051
//*                                                                 *   FILE1051
//*     Moreover, zEMF provides the capability for System           *   FILE1051
//*     Programmers to classify resource usage by JOBs, Started     *   FILE1051
//*     Tasks, and TSO sessions, supporting the usage of generic    *   FILE1051
//*     names for each.  For instance, they can designate JOB A     *   FILE1051
//*     to utilize unlimited CPU resources while restricting JOB    *   FILE1051
//*     B to limited CPU resources.  Similarly, they can            *   FILE1051
//*     allocate limited CPU resources to a specific category of    *   FILE1051
//*     TSO users while granting unlimited CPU resources to         *   FILE1051
//*     another category.  This granular control over resource      *   FILE1051
//*     allocation facilitates efficient management of system       *   FILE1051
//*     resources based on specific workload requirements.          *   FILE1051
//*                                                                 *   FILE1051
```
