# SFTP-RFC913
Implementing Simple File Transfer in Java

Objective: Implementing a file transfering protocol, SFTP (Simple File Transfer Protocol) in Java.

SFTP Credit: https://tools.ietf.org/html/rfc913

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
