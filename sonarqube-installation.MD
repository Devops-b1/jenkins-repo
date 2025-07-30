Prerequisites Istallatio.
Install Java 11
apt update -y
apt install openjdk-11-jdk -y
Install Postgresql
apt install postgresql -y
systemctl start postgresql
systemctl enable postgresql
Cofigure Linux
sysctl -w vm.max_map_count=524288
sysctl -w fs.file-max=131072
ulimit -n 131072
ulimit -u 8192
Deploy Schema
sudo -u postgres psql template1
CREATE USER sonarqube;
ALTER USER sonarqube with encrypted password 'Redhat123';
CREATE DATABASE sonarqube;
enter into database
\c sonarqube
GRANT ALL PRIVILEGES ON DATABASE sonarqube TO sonarqube;
GRANT ALL ON SCHEMA public TO sonarqube;
Install Sonarqube server
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.8.100196.zip
apt install unzip -y
unzip sonarqube-9.9.8.100196.zip
mv sonarqube-9.9.8.100196 /opt/sonarqube
vi conf/sonar.properties sonar.jdbc.username=sonarqube sonar.jdbc.password=mypassword sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
apt install openjdk-17-jdk
useradd sonar
chown -R sonar:sonar /opt/sonarqube
su sonar
bin/linux/sonar.sh start



to start sonarqube
/opt/sonar/bin/linux-x86-64/sonar.sh start

to show status
/opt/sonar/bin/linux-x86-64/sonar.sh status

to get logs
less logs/sonar.log