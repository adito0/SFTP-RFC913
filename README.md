# SFTP-RFC913
Implementing Simple File Transfer in Java

Objective: Implementing a file transfering protocol, SFTP (Simple File Transfer Protocol) in Java.

SFTP Credit: https://tools.ietf.org/html/rfc913

### To run:


### Commands:

The following commands have been implemented:
* USER - Authenticates the user type e.g admin/student/staff
* ACCT - Authenticates account username
* PASS - Authenticates corresponding account password
* TYPE - Specifies file storage
* LIST - Lists files in current directory
* CDIR - Changes directories
* KILL - Deletes a file in the current directory
* NAME - Renames a file in the current directory
* DONE - Closes connection
* RETR - Retrieves file and saves it at a user specified location
* STOR - Sends a file and stores is according to user preference

### Files provided:

#### accountData.txt
```
UserID	   AcctID	      Paswrd
admin
student	  aram485	      hi*pg3r3
student	  pdac546	      hj*ph3r4
student	  pku678	      hi*ph3r7
staff	    aram675	      hi*tg3r5
staff	    fgru877	      hj*tg3r6
guest	    hgi4756	      hj*pg3r9
IT
```
