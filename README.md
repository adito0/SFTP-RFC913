# SFTP-RFC913

Objective: Implementing a file transfering protocol, SFTP (Simple File Transfer Protocol) in Java.

SFTP Credit: https://tools.ietf.org/html/rfc913

This has been developed using JDK.14 on IntelliJ 2020. The application runs on localhost.

### To run:
There are two ways to run this. Firstly through the .jar file. However this cannot be used if we want to check the the output in the case that an account_data.txt file does not exist.

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

For all these commands, either uppercase or lowercase is acceptable. Parameters following the commands do not all have this feature.

### Files provided:

#### accountData.txt
A sample text file representing valid accounts. If a UserID has full access without requiring an account or password these fields will be blank e.g. admin.

NOTE: This file must be in the same package as the server package in order to run.
```
UserID - AcctID - Paswrd
admin
student - aram485 - hi*pg3r3
student - pdac546 - hj*ph3r4
student - pku678 - hi*ph3r7
staff - aram675 - hi*tg3r5
staff - fgru877 - hj*tg3r6
guest - hgi4756 - hj*pg3r9
IT
```
#### Test files
* toSend.txt - A sample text file that can be sent to the client.
* toReceive1.txt - A sample text file that can be sent to the server.
* toReceive2.txt - Another sample text file that can be sent to the server.
* toappend.txt - A sample text file that can be appended to an existing file.

### Test cases:

#### Init
Upon starting the client, the following should be visible if the client could successfully make a socket.
```
Cannot make socket: IOException.
```
If the client successfully connects with the server, the following messge should appear in the client terminal.
```
+MyServer SFTP Service
```
Otherwise, the following error message will show.
```
-server@<port> Out to Lunch
```
Upon starting the server, nothing should appear. If the account data file does not exist the following error message will show up. Ensure it is in the same folder as the server package.
```
Cannot find account data text file!
```

#### USER <user_id>
This authenticates the user into the system. Each user type has different privledges which full be further discussed as we go along.
```
$ USER admin
!admin logged in
```
```
$ USER student
+User-id valid, send account and password
```
```
$ USER tree
-Invalid user-id, try again
```
```
$ USER
-Invalid user-id, try again
```


The server's directory by default is set to where the project folder is saved. This can be changed using the CDIR command which will be discussed later. However to check initial directory:
```
$ LIST F

```

