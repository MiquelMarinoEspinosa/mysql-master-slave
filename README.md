Basic mysql master slave project.
- Requirements: vagrant and ansible

- Setup the vagrant environment
vagrant up

- Log in into the mysql-master machine
vagrant ssh mysql-master

- Check the status of the master data base
mysql -u root
SHOW MASTER STATUS;

- Copy the file and the position values
+------------------+----------+--------------+------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+------------------+----------+--------------+------------------+
| mysql-bin.000001 |      264 | test         |                  |
+------------------+----------+--------------+------------------+

- Log out from master-mysql vagrant machine
exit
exit

- Log in into the master-slave vagrant machine
vagrant ssh mysql-slave

- Configure the mysql slave with the file and position previously copied
mysql -u root
CHANGE MASTER TO MASTER_HOST='172.21.99.4',MASTER_USER='slave_user', MASTER_PASSWORD='slave_user', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=264;
START SLAVE

- Check there are no records yet in the slave data base
USE test;
SELECT * FROM Test;

- Log out from the slave machine
exit
exit

- Log in into the master machine
vagrant ssh mysql-master

- Insert a new row into the the Test table
mysql -u root
USE test;
INSERT INTO Test (content) VALUES ("I am a master record!");
SELECT * FROM Test;

- Log out from the mysql-master
exit
exit

- Log in into the mysql-slave
vagrant ssh mysql-slave

- Check that the record has been sync from master to slave
mysql -u root
USE test;
SELECT * FROM test; 
