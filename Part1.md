### Part1


#### 1. Check PreQual
```
$ cat /proc/sys/vm/swappiness
$ cat /sys/kernel/mm/transparent_hugepage/defrag
$ cat /sys/kernel/mm/transparent_hugepage/enabled
$ sudo vi /etc/selinux/config
$ sudo systemctl status nscd
$ sudo systemctl status ntp
```
![Alt text](/Part1/img/1_CheckPreQual.PNG)

#### 2. Hosts Setup
```
172.31.41.215 cm.com cm
172.31.32.211 nn.com nn
172.31.36.254 dn1.com dn1
172.31.36.87 dn2.com dn2
172.31.37.61 dn3.com dn3
```
![Alttext](/Part1/img/2_hostsSetup.PNG)

#### 3. JDK Install
```
$ sudo yum install java-1.8.0-openjdk-devel.x86_64
```
![Alttext](/Part1/img/3_jdkInstall.PNG)

#### 4. JDBC Install
```
$ cd ~
$ sudo yum install wget
$ wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.46.tar.gz
$ tar zxvf mysql-connector-java-5.1.46.tar.gz
$ sudo mkdir -p /usr/share/java/
$ cd mysql-connector-java-5.1.46
$ sudo cp mysql-connector-java-5.1.46-bin.jar /usr/share/java/mysql-connector-java.jar
```
![Alttext](/Part1/img/4_JDBCInstall.PNG)

#### 5. Centos Password Setup
```
$ sudo passwd centos
   비밀번호 training
$ sudo vi /etc/ssh/sshd_config
   change -> PasswordAuthentication yes
$ sudo systemctl restart sshd.service
```
![Alttext](/Part1/img/5_CentosPasswordSetup.PNG)

#### 6. HostName Setup
![Alttext](/Part1/img/5_hostnameSetup.PNG)

#### 7. Ping And GetEnt
![Alttext](/Part1/img/6_pingAndgetent.PNG)

#### 8. MariaDB Install And CreateDB
```
$ sudo yum install mariadb-server
$ cd /usr/bin
$ ll
$ sudo systemctl enable mariadb
$ sudo systemctl start mariadb
$ sudo ./mysql_secure_installation

$ mysql -u root -p
CREATE DATABASE scm DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON scm.* TO 'scm-user'@'%' IDENTIFIED BY 'somepassword';
CREATE DATABASE amon DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON amon.* TO 'amon-user'@'%' IDENTIFIED BY 'somepassword';
CREATE DATABASE rmon DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON rmon.* TO 'rmon-user'@'%' IDENTIFIED BY 'somepassword';
CREATE DATABASE hue DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON hue.* TO 'hue-user'@'%' IDENTIFIED BY 'somepassword';
CREATE DATABASE metastore DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON metastore.* TO 'metastore-user'@'%' IDENTIFIED BY 'somepassword';
CREATE DATABASE sentry DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON sentry.* TO 'sentry-user'@'%' IDENTIFIED BY 'somepassword';
CREATE DATABASE oozie DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL ON oozie.* TO 'oozie-user'@'%' IDENTIFIED BY 'somepassword';
FLUSH PRIVILEGES;
SHOW DATABASES;
EXIT;
```
![Alttext](/Part1/img/7_mariaDBinstallAndCreateDB.PNG)

#### 9.  Configure Cloudera Manager
```
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64           	  
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.15.2/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera    
gpgcheck = 1

$ sudo yum install cloudera-manager-server cloudera-manager-daemons

$ sudo /usr/share/cmf/schema/scm_prepare_database.sh mysql scm scm-user somepassword

$ sudo systemctl start cloudera-scm-server

$ sudo systemctl status cloudera-scm-server
```
![Alttext](/Part1/img/8_baseUrlSetup.PNG)

#### 10. CM Login(IP : 13.125.177.69)
```
13.125.177.69:7180
```
![Alttext](/Part1/img/9_CM_Login.PNG)

#### 11. Host 지정
![Alttext](/Part1/img/10_CM_HostList.PNG)

#### 12. SSH Login
![Alttext](/Part1/img/11_CM_LoginSetup.PNG)

#### 13. Parcel Install
![Alttext](/Part1/img/12_CM_ParcelInstall.PNG)

#### 14. 정확성 검사
![Alttext](/Part1/img/13_CM_호스트정확성검사.PNG)

#### 15. Select Services
![Alttext](/Part1/img/14_CM_SelectServices.PNG)

#### 16. 역할 할당
![Alttext](/Part1/img/15_CM_역할할당.PNG)

#### 17. DataBase 설정
![Alttext](/Part1/img/16_CM_DataBaseSetup.PNG)

#### 18. 클러스트 설정 - 첫 번째 실행 명령
![Alttext](/Part1/img/17_CM_Complete.PNG)

#### 19. CM Main 화면
![Alttext](/Part1/img/18_CM_Complete_2.PNG)

#### 20. Window -> CM(training) User 홈 화면에 author, posts sql 파일 전송
![Alttext](/Part1/img/19_CM_MoveSql.PNG)

#### 21. Create test DB
```
use test
source posts.sql
source authors.sql
```
![Alttext](/Part1/img/20_CM_testDB.PNG)

#### 22. Sqoop To Hive Posts And Authors 테이블
![Alttext](/Part1/img/21_HUE_SqoopToHive.PNG)

#### 23. Hue에서 Posts, Authors 테이블 Select 및 Count 실행
![Alttext](/Part1/img/22_HUE_Hive_Query_Result.PNG)
