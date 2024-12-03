## Small Example Programs

Since this documentation is boring, we have added the good old "learn by example" section.



## Basic Job / Network Information

This program shows off a couple of useful commands, 
**RTVJOBA** (Retrieve Job Attributes) and **RTVNETA** (Retrieve Network Attributes) that expose a lot of cool data.

In this case we grab job name, user id, job number, and system name with two commands.
For a prettier output, we concatenate job name, user id, and job number to the format **12345/SOMEUSER/SOMEJOB**.
Finally, all we do is output everything I gathered to the console.

More information on these commands can be found here:
  * RTVJOBA - https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_71/cl/rtvjoba.htm
  * RTVNETA - https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_71/cl/rtvneta.htm

```php
/* JOBINFO.CLLE */

PGM                                                     
  DCL VAR(&username) TYPE(*CHAR) LEN(10)                 
  DCL VAR(&jobname)  TYPE(*CHAR) LEN(10)                 
  DCL VAR(&jobnum)   TYPE(*CHAR) LEN(6)                  
  DCL VAR(&jobtype)  TYPE(*CHAR) LEN(1)                  
  DCL VAR(&sysname)  TYPE(*CHAR) LEN(8)                  
                                                        
  /* Job type:  0=batch, 1=interactive */    
  RTVJOBA JOB(&jobname) CURUSER(&username) NBR(&jobnum) +
    TYPE(&jobtype) 

  RTVNETA SYSNAME(&sysname)                              
                                                        
  SNDUSRMSG MSG(&jobnum  *TCAT '/' +                    
            || &username *TCAT '/' +                    
            || &jobname)       
                               
  SNDUSRMSG MSG(&jobtype)                               
  SNDUSRMSG MSG(&sysname)       
                                                    
ENDPGM
```


## Calling a System API
To call a system API, you just have to match the parms and call it like a normal program.
This example uses the QUILNGTX (Long Text) API to show a simple popup message.


```php
/* CLPOPUP.CLLE */

PGM
  /*         QUILNGTX Prototype           */
  DCL VAR(&message)  TYPE(*CHAR) LEN(6800)
  DCL VAR(&length)   TYPE(*INT)  LEN(4)
  DCL VAR(&msgId)    TYPE(*CHAR) LEN(7)    VALUE('Test')
  DCL VAR(&qualmsgf) TYPE(*CHAR) LEN(20)   VALUE('Popup Message')
  DCL VAR(&nullErr)   TYPE(*PTR)  ADDRESS(*NULL)

  CHGVAR VAR(&message) +
    VALUE('This is a popup message using the QUILNGTX' +
      *BCAT 'API, its pretty neat.')

  CHGVAR VAR(&length) VALUE(%len(&message))

  CALL PGM(QSYS/QUILNGTX) PARM(&message &length &msgId +
                               &qualmsgf &nullErr)

ENDPGM
```


## Calling a SQL Stored Procedure
A stored procedure on IBMi can be treated like a callable program.
Once again, you match the parms and your good to go. You can also still fully use output parms as well.

```php
/* SQLPROC.CLLE */

PGM
  DCL VAR(&parm1)    TYPE(*INT)  LEN(4)
  DCL VAR(&outparm1) TYPE(*CHAR) LEN(64)

  /* Just match the parms of the stored proc */
  CALL PGM(SOMESTOREDPROC) PARM(&parm1 &outparm1)

  SNDUSRMSG MSG(&outparm1)

ENDPGM
```


## Using Bash in CL
IBMi comes with multiple shells installed. Sometimes its easier to take an existing shell script
and call it using CL. If you don't know any Bash, you should think about adding it to your toolbox.

Here are a few examples of fun things you can do. Since you have access to bash, the possibilities are endless.

```php
/* BASHTEST.CLLE */

PGM
  
  /* Running a basic command */
  QSH CMD('echo "hello world"')

  /* Executing a shell script */
  QSH CMD('./some_script.sh')

  /* Finding files in IFS directory by type */
  QSH CMD('find /home/otteb/ -name "*.PDF" -type f')

  /* Executing CL from bash, just because you can! */
  QSH CMD('system "DSPLIBL"')

ENDPGM
```


## Calling CL and QShell from Bash
We showed in the above example that you can call CL from bash, so let us show a clearer example.

IBMi also has another flavor of shell, QShell. It pretty much works as expected of a shell.
More on QShell can be read at https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzahz/rzahzpdf.pdf

With this new knowledge, you can create some really powerful utilities. For example, create a "generic" build script
using bash and QShell at https://gist.github.com/barrettotte/278e1e97fc2ba23c7ad6366b0b4c8668


```shell
#!/QOpenSys/pkgs/bin/bash

# /home/otteb/test.sh

# Display library list using CL
system "DSPLIBL"

# Display library list using QSH
qsh -c "liblist"

```
