# Debugging Batch Jobs (WIP)

In interactive jobs, you're directly connected to the job because you're actively working within that job's environment. Batched jobs run independently in the background, typically without any direct user interface. That's why we need to catch it.

## Finding the Batch Job

1. Use ```WRKACTJOB``` or ```WA``` (Work with Active Jobs) command to locate your batch job.

    If you know the job name, press F4 and specify JOB parameter
    Otherwise, look for your job in the active jobs list
    Note down: Job Name, User, and Number (format: 123456/USERNAME/JOBNAME)

    *TIP: Sometimes it can help to run the job & see the CPU usage to identify the correct job.*

## Starting Debug Session

1. First, start service job using STRSRVJOB (Start Service Job):<br>
    ```STRSRVJOB JOB(123456/USERNAME/JOBNAME)```
2. Then start debug using STRDBG (Start Debug):<br>
    ```STRDBG PGM(MYLIB/MYPGM)```
3. Find and set a breakpoint to the source code. (Press ```F6``` on a line of source code.)

## Viewing Program Stack

Use ```DSPDBG``` (Display Debug) to see:
* Current program stack
* Active breakpoints
* Program variables

## Ending Debug Session

1. End debug mode:<br>
```ENDDBG```
2. End service job:<br>
```ENDSRVJOB```

## Troubleshooting Tips

**1. If STRSRVJOB fails:**
* Ensure the debug mode has been ended. (enddbg)
* Verify job is still active
* Check your authority to the job
* Ensure no other user is servicing the job


**2. If STRDBG fails:**
* Verify program exists in specified library
* Check program debug data exists (CHGPGM DBGVIEW(*SOURCE))
* Ensure program is not already being debugged


**3. Common Error Messages:**
* CPF0164: Debug session ended abnormally
* CPF1440: Not authorized to service job
* CPF1468: Cannot start debug because job is already being debugged