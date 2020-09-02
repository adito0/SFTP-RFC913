# SFTP-RFC913

Objective: Implementing a file transfering protocol, SFTP (Simple File Transfer Protocol) in Java.

SFTP Credit: https://tools.ietf.org/html/rfc913

This has been developed using JDK.14 on IntelliJ 2020. The application runs on localhost.

### To run:
There are two ways to run this. Firstly through the .jar file. Open two terminals and in one go to where the server's far file is saved. In the other go to where the client's jar file is saved. To run command: java -jar test.jar. Both of these jar files are in a folder called "test". NOTE: Ensure the data.txt file is in the same place as the server's jar file. The other way to run this is through an IDE like eclipse. If the jar files don't work try this method. The files are in SFTP_725A1. This project has been verified to work with IntelliJ on the Windows OS. Once again ensure that data.txt is in the same package as the server's main class. 

### Commands:

The following commands have been implemented:
* USER - Authenticates the user type e.g admin/student/staff
* ACCT - Authenticates account username
* PASS - Authenticates corresponding account password
* TYPE - Specifies file storage
* LIST - Lists files in current directory
* CDIR - Changes directories
* KILL - Deletes a file in the current directory
* NAME/TOBE - Renames a file in the current directory
* DONE - Closes connection
* RETR/SEND - Retrieves file and saves it at a user specified location
* STOR/SIZE - Sends a file and stores is according to user preference

For all these commands, either uppercase or lowercase is acceptable. Parameters following the commands do not all have this feature.

### Files provided:

#### data.txt
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
#### Testing Folder files
* toSend.txt
* greetings.txt
* hello.txt
* blank.docx
* aSmolFolder
#### Other testing files - please save this somewhere else on your computer
* toReceive.txt
* greetings.txt

Greetings.txt are two different files. Please save one of them somewhere else. 


### Test cases:

#### Init
Upon starting the client, the following should be visible if the client could not successfully make a socket.
```
Cannot make socket: IOException
```
If the client successfully connects with the server, the following message should appear in the client terminal.
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
If a correct command is not given at any point, the following message should appear.
```
-Try again
```

#### USER <user_id>
This authenticates the user into the system. Each user type has different privledges. In the sample account data, admin and IT do not have to sign in with an account and password.
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

#### ACCT <account_id>
This authenticates the account into the system. A user id must be specified prior, otherwise an error message will show.
```
$ USER admin
!admin logged in
$ ACCT
!Account not needed, logged-in
$ ACCT test
!Account not needed, logged-in
```
```
$ USER student
+User-id valid, send account and password
$ ACCT
-Invalid account, try again
$ ACCT invalidAccount
-Invalid account, try again
$ ACCT aram675
-Invalid account, try again
$ ACCT aram485
+Account valid, send password
```
```
$ USER student
+User-id valid, send account and password
$ ACCT invalidAccount
-Invalid account, try again
$ ACCT aram675
-Invalid account, try again
$ ACCT aram485
+Account valid, send password
```
```
$ ACCT aram485
-Invalid account, please specify your User ID first
```

#### PASS <pass_word>
This is the final step in the authentication process. Invalid passwords can be tested, for brevityonly one is shown below. The last test will ensure that the password can be asked before an account authentication, and if another account not associated with the password is given, the password for that account will be asked.
```
$ USER admin
!admin logged in
$ PASS invalid
!Password not needed, logged-in
```
```
$ USER student
+User-id valid, send account and password
$ ACCT aram485
+Account valid, send password
$ PASS one1
! Logged in
```
```
$ USER staff
+User-id valid, send account and password
$ PASS invalid
-Wrong password, try again
$ PASS four4
+Send account
$ ACCT fgru877
+Account valid, send password
$ PASS five5
! Logged in
```
*The following commands can only be used once the user has been fully authenticated. The response for not logging in before any of these commands is shown once, but will be identical in every case.*

#### LIST <V_or_F> <full_directory_path>
This lists the files in a specified directory in two potential formats, V, or F. If no directory is specified, or the directory doesn't exist, the list of files in the current directory will be displayed. There is a folder provided with 3 test files. Copy and paste this directory any where onto your computer and copy the path.
```
$ LIST  F C:\Users\user\Desktop\Testing
-Please log in
```
```
$ USER admin
!admin logged in
$ LIST F C:\Users\user\Desktop\Testing
+C:\Users\user\Desktop\Testing
aSmolFolder
blank.docx
hello.txt
```
```
$ USER admin
!admin logged in
$ LIST v
+C:\Users\user\Downloads\SFTP_725A1
.idea		4KB		Wed Sep 02 11:09:07 NZST 2020
out		0KB		Thu Aug 27 01:57:47 NZST 2020
SFTP_725A1.iml		0KB		Thu Aug 27 01:54:28 NZST 2020
src		0KB		Tue Sep 01 20:40:38 NZST 2020
```

#### TYPE <A_or_B_or_C>
This tells the server how to store the files. A = Ascii, B = Binary, C= Continuous.
```
$ USER admin
!admin logged in
$ TYPE A
+Using Ascii mode
$ TYPE B
+Using Binary mode
$ TYPE C
+Using Continuous mode
```

#### CDIR <full_directory_path>
This changes the current directory. By default the server's directory is set to where the project folder is saved. If the user has full access (through an admin or IT account) they will not be expected to reauthenticate. Otherwise, they will need to re-enter their credentials.
```
$ USER admin
!admin logged in
$ CDIR invalid
-Can't connect to directory because it does not exist
```
```
$ USER admin
!admin logged in
$ CDIR C:\Users\user\Desktop\
!Changed working dir to C:\Users\user\Desktop\
```
```
$ USER student
+User-id valid, send account and password
$ ACCT aram485
+Account valid, send password
$ PASS one1
!Logged in
$ CDIR C:\Users\user\Desktop\Testing
+directory ok, send account/password
$ ACCT aram485
+Account valid, send password
$ PASS one1
! Logged in
!Changed working dir to C:\Users\user\Desktop\Testing
```

#### KILL <file_name>
Deletes a file in the current directory. In the following test case, hello.txt should no longer exist.
```
$ USER admin
!admin logged in
$ CDIR C:\Users\user\Desktop\Testing
!Changed working dir to C:\Users\user\Desktop\Testing
$ LIST f
+C:\Users\user\Desktop\Testing
aSmolFolder
blank.docx
hello.txt
$ KILL hello.txt
+hello.txt deleted
$ KILL
-Not deleted because: Does not exist
$ KILL aSmolFolder
-Not deleted because not a valid file
```
#### NAME <file_name>
Saves the name of the file to be renamed from the current directory.
```
$ USER admin
!admin logged in
$ CDIR C:\Users\user\Desktop\Testing
!Changed working dir to C:\Users\user\Desktop\Testing
$ LIST f
+C:\Users\user\Desktop\Testing
aSmolFolder
blank.docx
hello.txt
$ NAME blank.docx
+File exists
$ NAME
-Please specify filename
$ NAME bye.txt
-Can't find bye.txt
```
#### TOBE <file_name>
Renames the file from NAME above.
```
$ USER admin
!admin logged in
$ CDIR C:\Users\user\Desktop\Testing
!Changed working dir to C:\Users\user\Desktop\Testing
$ NAME blank.docx
+File exists
$ TOBE word.docx
+blank.docx renamed to word.docx
$ NAME word.docx
+File exists
$ PASS
!Password not needed, logged-in
$ TOBE blank.docx
-File wasn't renamed because the new name must be given straight after the cmd NAME
$ NAME word.docx
+File exists
$ TOBE *
-File wasn't renamed because the name is not valid
 ```
#### DONE
Closes the connection.
```
$ DONE
+MyServer stopped.
```

#### RETR <file_name>
Retrieves a file for transfer from the current directory and displays the size. If the user has enough space to save the file they must use the SEND command.
```
$ USER admin
!admin logged in
$ CDIR C:\Users\user\Desktop\Testing
!Changed working dir to C:\Users\user\Desktop\Testing
$ RETR invalid
-File doesn't exist
```
```
$ USER admin
!admin logged in
$ CDIR C:\Users\user\Desktop\Testing
!Changed working dir to C:\Users\user\Desktop\Testing
$ RETR toSend.txt
60
```
#### SEND
This command verifies that the file should be sent. The user should use this straight after the RETR if they believe their system has enough space.
```
$ RETR toSend.txt
60
$ SEND
$ Specify a location to save: 
C:\Users\user\Desktop
$ Specify a name to save as
saved.txt
+Send successful
```
#### STOP
This command aborts the retrieval of a file. The user should use this straight after the RETR if they believe their system does not have enough space.
```
$ RETR toSend.txt
60
$ STOP
+ok, RETR aborted
```
#### STOR <NEW_or_OLD_or_APP> <file_name>
This command send a file to the server to save it in the server's current directory. If there is an existing file with the same name the user can choose to create a new generation (NEW), overwrite the existing file (OLD), or append to the existing file (APP). Appending only works for text files.
```
$ STOR NEW C:\Users\user\Desktop\toReceive.txt
Size of file: 57
+File does not exist, will create new file
```
```
$ STOR NEW C:\Users\user\Desktop\greetings.txt
Size of file: 8
+File exists, will create new generation of file
```
```
$ STOR OLD C:\Users\user\Desktop\greetings.txt
Size of file: 8
+File exists, will write over old file
```
```
$ STOR NEW C:\Users\user\Desktop\greetings.txt
Size of file: 8
+File exists, will append to file
```
#### SIZE <size_specified>
This command sends this size of the file so that the server can either accept the file, if it has enough space, or abort the transfer. If the file is accepted it will confirm that it has received the file. The size should be exactly what was printed out under the STOR command.
```
$ STOR OLD C:\Users\user\Desktop\toReceive.txt
Size of file: 57
+File exists, will create new file
$ SIZE 57
+ok waiting for file
+Saved toReceive.txt
```
```
$ STOR OLD C:\Users\user\Desktop\greetings.txt
Size of file: 8
+File exists, will write over old file
$ SIZE 8
+ok waiting for file
+Saved greetings.txt
```
```
$ STOR NEW C:\Users\user\Desktop\greetings.txt
Size of file: 8
+File exists, will create new generation of file
$ SIZE 8
+ok waiting for file
+Saved greetings(1).txt
```
```
$ USER admin
!admin logged in
$ CDIR C:\Users\user\Desktop\Testing
!Changed working dir to C:\Users\user\Desktop\Testing
$ STOR APP C:\Users\user\Desktop\greetings.txt
Size of file: 8
+File exists, will append to file
$ SIZE 8
+ok waiting for file
+Saved greetings.txt
```
