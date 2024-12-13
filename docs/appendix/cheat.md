# Cheat Sheet (WIP)
A cheat sheet of useful commands.

## Programming Development Manager (PDM)
| Command | Description |
|---------|-------------|
| ```STRPDM``` | Start Programming Development Manager |
| ```WRKPGM``` | Work with Programs |
| ```WRKMBRPDM``` | Work with Members Using PDM |
| ```WRKOBJPDM``` | Work with Objects Using PDM |
| ```STRSEU``` | Start Source Entry Utility |
| ```WRKLIBPDM``` | Work with Libraries Using PDM |

## Debugging and Testing
| Command | Description |
|---------|-------------|
| ```STRDBG``` | Start Debug Mode |
| ```ENDDBG``` | End Debug Mode |
| ```STRISDB``` | Start Interactive SQL Debug |
| ```STRSRVJOB``` | Start Service Job |
| ```ENDSRVJOB``` | End Service Job |
| ```ADDBKP``` | Add Breakpoint |
| ```RMVBKP``` | Remove Breakpoint |
| ```WRKBKP``` | Work with Breakpoints |
| ```TRCJOB``` | Trace Job |
| ```DSPMODSRC``` | Display Module Source |
| ```DSPJOB``` | Display Job |
| ```WRKJOB``` | Work with Job |
| ```DSPJOBLOG``` | Display Job Log |
| ```SNDDTAARA``` | Send Data Area |
| ```DSPDTAARA``` | Display Data Area |
| ```CHGDTAARA``` | Change Data Area |

## IFS 
| Command | Description |
|---------|-------------|
| ```GO CMDLNK``` | Go to Link Commands |
| ```WRKLNK``` | Work with Links |
| ```DEL``` | Remove Link |
| ```MOV``` | Move Object |
| ```RNM``` | Remove Object |
| ```QShell``` or ```QSH``` | Start QSH |

## Library List
| Command | Description |
|---------|-------------|
| ```ADDLIBLE``` | Add library to the library list |
| ```RMVLIBLE``` | Remove library to the library list |
| ```DSPLIBLE``` | Display library list |
| ```EDTLIBL``` | Edit library list |
| ```CHGLIBL``` | Change library list |
| ```CHGSYSLIBL``` | Change System Library List |
| ```CHGCURLIB``` | Change current library |

## Objects and Libraries
| Command | Description |
|---------|-------------|
| ```CRTLIB``` | Create library |
| ```DLTLIB``` | Delete library |
| ```DSPLIB``` | Display library |
| ```DSPLIBD``` | Display library description |
| ```CHGLIB``` | Change library |
| ```WRKLIB``` | Work with libraries |
| ```DSPOBJD``` | Display object description |
| ```CHGOBJD``` | Change object description |
| ```CRTDUPOBJ``` | Create duplicated object |
| ```WRKOBJ``` | Work with objects |

## Database
| Command | Description |
|---------|-------------|
| ```RUNSQL``` | Run SQL sentence |
| ```STRSQL``` | Start SQL interactive session |
| ```STRQM``` | Start Query Manager |
| ```WRKQRY``` | Work with queries |
| ```DSPPFM``` | Display physical file member |
| ```CRTPF``` | Create physical file |
| ```DLTF``` | Delete file |
| ```WRKRDBEDIRE``` | Work with Relational Database Directory Entries |
| ```STRDBMON``` | Start database monitor |

## Back-up and Recovery
| Command | Description |
|---------|-------------|
| ```RST``` | Restore IFS Object |
| ```SAV``` | Save IFS Object |
| ```SAVOBJ``` | Save Object |
| ```SAVLIB``` | Save Library |
| ```RSTOBJ``` | Restore Object |
| ```RSTLIB``` | Restore Library |
| ```CRTSAVF``` | Create Save File |
| ```GO SAVE - Opc 21``` | Full System Back-up |
| ```EDTRCYAP``` | Edit recovery for access paths |

## Communications
| Command | Description |
|---------|-------------|
| ```NETSTAT``` | Work with TCP/IP network status |
| ```CFGTCP``` | Configure TCP/IP menu |
| ```CFGTCPAPP``` | Configure TCP/IP application menu |
| ```STRTCPSVR``` | Start TCP Server |
| ```ENDTCPSVR``` | End TCP Server |
| ```FTP``` | Start FTP transfer |
| ```PING``` | Verify TCP/IP connection |
| ```TRACEROUTE``` | Trace TCP/IP route |

## Job Management
| Command | Description |
|---------|-------------|
| ```WRKACTJOB``` or ```WA``` | Work with active jobs |
| ```WRKUSRJOB``` | Work with jobs for a given user |
| ```SBMJOB``` | Submit job |
| ```TFRJOB``` | Transfer job |
| ```WRKJOBSCDE``` | Work with job schedule entries |
| ```WRKJVM``` | Work with Java Virtual Machine jobs |
| ```WRKSBS``` | Work with subsystems |
| ```WRKSBSD``` | Work with subsystem descriptions |
| ```WRKJOBQ``` | Work with job queues |
| ```WRKJOBD``` | Work with job descriptions |
| ```WRKCLS``` | Work with class |
| ```STRSRVJOB``` | Start Service Job (Debug)|
| ```ENDSRVJOB``` | End Service Job (Debug) |

## System Logs
| Command | Description |
|---------|-------------|
| ```DSPLOG``` | Display log |
| ```DSPJOBLOG``` | Display job log |
| ```DSPMSG QSYSOPR``` | Display system operator message queue |
| ```NETSTAT *CNN``` | Work with IPv4 connections status |

## Printing and Spooling
| Command | Description |
|---------|-------------|
| ```WRKSPLF``` or ```SP``` | Work with spool files |
| ```SNDTCPSPLF``` | Send spool file via TCPIP |
| ```WRKOUTQ``` | Work with output queues |
| ```STRPRTWTR``` | Start printer writer |
| ```STRRMTWTR``` | Start remote writer |
| ```ENDWTR``` | End writer |
| ```WRKDEVD *PRT``` | Work with printer devices |

## Authorities
| Command | Description |
|---------|-------------|
| ```DSPAUT``` | Display IFS object authority |
| ```CHGAUT``` | Change IFS object authority |
| ```CHGOWN``` | Change IFS object owner |
| ```DSPOBJAUT``` | Display object authority |
| ```CHGOBJAUT``` | Change object authority |
| ```GRTOBJAUT``` | Grant object authority |
| ```RVKOBJAUT``` | Revoke object authority |
| ```CHGOBJOWN``` | Change object owner |
| ```WRKAUTL``` | Work with authorization lists |

## User Admin
| Command | Description |
|---------|-------------|
| ```WRKUSRPRF``` | Work with user profiles |
| ```DSPUSRPRF OPTION(*GRPMBR)``` | Display user profile (group membership) |
| ```WRKDIRE``` | Work with directory entries |
| ```DSPUSRPMN``` | Display user permissions (email) |
| ```GRTUSRPMN``` | Grant user permissions (email) |
| ```RVKUSRPMN``` | Revoke user permissions (email) |