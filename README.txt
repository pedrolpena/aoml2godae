

The linkArgoFiles script iterates through AOML's ftp argo data folder creating hard links 
to these files in locations that mimics GODAE's ftp argo data directory structure.
Hard links allow multiple files to point to the same data avoiding the multiple copies.
The original files can be deleted after the links are created and the data will not be lost.
This script has to be run where the files are located so it runs on AOML's public ftp server.

Currently the script will list and link files that are 5 days old or younger from the time it is run.
The script logs links created and deleted in a log file named "linkArgoFiles.log"

The source,target and log directories have to specified by setting the following variables.

sourceDirectory="someDirectoryPath"
targetDirectory="someOtherDirectoryPath"
logDir="yetAnotherDirectoryPath/"

Note how the "logDir" variable ends in a "/", and sourceDirectory and targetDirectory do not. 
This is intentional and necessary because of the way the script is written.


 
Here is an example of what the script does.


Assume nc is the source directory with sub directories and files.

|--[nc]-
|      |-[aoml]-
|      |       |-[tmp]
|      |       |
|      |       |-13857_meta.nc
|      |       |-13857_tech.nc
|      |       |-13857_traj.nc
|      |       |-R13857_001.nc
|      |       |-R13857_002.nc
|      |       |-R13857_003.nc
|      |       |-R13857_004.nc
|      |       |-     *
|      |       |-     *
|      |       |-     *
|      |
|      |
|      |
|      |
|      |---[uw]-
|              |-[tmp]
|              |
|              |-13859_meta.nc
|              |-13859_tech.nc
|              |-13859_traj.nc
|              |-R13859_001.nc
|              |-R13859_002.nc
|              |-R13859_003.nc
|              |-R13859_004.nc
|              |-     *
|              |-     *
|              |-     *
|
*
*
*

Assuming the target directory is Nu_nc, the script will create a directory structure with the following hard links in it.

|--[Nu_nc]-
|         |-[aoml]-
|         |       |-[13857]-
|         |                |
|         |                |-13857_meta.nc
|         |                |-13857_tech.nc
|         |                |-13857_traj.nc
|         |                |
|         |                |-[profiles]-
|         |                            |-R13857_001.nc
|         |                            |-R13857_002.nc
|         |                            |-R13857_003.nc
|         |                            |-R13857_004.nc
|         |                            |-     *
|         |                            |-     *
|         |                            |-     *
|         |
|         |
|         |
|         |
|         |-[uw]-
|               |-[13859]-
|                        |
|                        |-13859_meta.nc
|                        |-13859_tech.nc
|                        |-13859_traj.nc
|                        |
|                        |-[profiles]-
|                                    |-R13859_001.nc
|                                    |-R13859_002.nc
|                                    |-R13859_003.nc
|                                    |-R13859_004.nc
|                                    |-     *
|                                    |-     *
|                                    |-     *
|         
*
*
*






