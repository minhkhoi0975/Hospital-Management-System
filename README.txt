How to run the project:

TL/DR: 
   + Extract the contents in the .zip file
   + Create a database from the .sql file
   + Make sure that mysql-connector-java-5.1.49.jar is in the project
   + Create a Tomcat server
   + Test the program

Detail:
1. Extract the contents in the .zip file

2. Create a database (very important because the Servlet program will not work if the database does not exist)
   + Open command prompt (cmd) and create a new database.
   + Close cmd, reopen it, and cd to the "bin" folder that contains mysqldump (e.g. cd C:/program files/MySQL/MySQL Server5.1/bin).
   + Use the command below to create a database from the .sql file:
     mysqldump -u[username] -p[password] [database name] < [full path of the .sql file]
     (e.g. mysqldump -uroot -proot hospitalmanagementsystem < C:/JavaProjects/HospitalManagementSystem/database/hospitalmanagementsystem.sql)

2'. If you are not familliar with mysqldump, you can do this way:
    + Open hospitalmanagementsystem.sql with notepad.
    + Open cmd and create a database.
    + In notepad, copy a "CREATE TABLE" statement, paste it to cmd, and press ENTER. Do the same thing for the remaining "CREATE TABLE" statements.

    A "CREATE TABLE" statement should look similar to this:
    
CREATE TABLE `appointment` (
  `appointmentID` int unsigned NOT NULL,
  `patientID` int unsigned NOT NULL,
  `doctorID` int unsigned NOT NULL,
  `roomID` int unsigned NOT NULL,
  `date` date NOT NULL,
  `startTime` time NOT NULL,
  `endTime` time NOT NULL,
  `note` varchar(300) DEFAULT NULL,
  PRIMARY KEY (`appointmentID`),
  UNIQUE KEY `appointmentID_UNIQUE` (`appointmentID`),
  KEY `patientID_idx` (`patientID`),
  KEY `doctorID_idx` (`doctorID`),
  KEY `roomID_idx` (`roomID`),
  CONSTRAINT `doctorID` FOREIGN KEY (`doctorID`) REFERENCES `doctor` (`doctorID`),
  CONSTRAINT `patientID` FOREIGN KEY (`patientID`) REFERENCES `patient` (`medicalRecordNumber`),
  CONSTRAINT `roomID` FOREIGN KEY (`roomID`) REFERENCES `room` (`roomID`)
)  

3. Open the project in NetBeans

4. Check dependency (This project uses mysql-connector-java-5.1.49.jar to get access to database. Make sure that it is included in the project.)
   In the "project" window, go to HospitalManagementSystem->Libraries and check if mysql-connector-java-5.1.49.jar exist.
   If they don't, right click, select "Add JAR/Folder..." and add this file to the project. It is in the "dependencies" folder.

5. Create a Tomcat server (A Servlet program cannot work without a server.)
   + In the menu bar, select Tools->Servers.
   + In the "Server" window, click the "Add Server..." button.
   + Select "Apache Tomcat or TomEE" and enter the server name, then click "Next".
   + For the "Server Location", enter the path to Apache Tomcat (e.g C:\JavaProjects\apache-tomcat-9.0.39).
   + Enter the username and password and select "Create user if it does not exist", then click "Finish".
   + In the "Server" window, make sure that the Server Port is 8080 and the Shutdown Port is 8005.
   
6. Test the program.
   + In the project window, select HospitalManagementSystem, right click and select "Run".
   + Enter the username and password of your Tomcat server.
   + Test the program.
   
If you have any problems, please email me (kdho@bhcc.edu).
For references, they are in the "references" folder.
