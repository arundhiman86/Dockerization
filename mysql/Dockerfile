#Set the base image to Ubuntu
FROM ubuntu:14.04

# Updating repositories
RUN apt-get update

# Build time variable arguments
ARG database_name
ARG table_name
ARG tomcat_user
ARG tomcat_ip
ARG tomcat_password
ARG mysql_username
ARG mysql_password

# update password information for mysql before installation
RUN echo "mysql-server-5.6 mysql-server/root_password password $mysql_password" | sudo debconf-set-selections
RUN echo "mysql-server-5.6 mysql-server/root_password_again password $mysql_password" | sudo debconf-set-selections

# Installing mysql server 5.6
RUN apt-get install -y mysql-server-5.6

# Configuring mysql
RUN service mysql start && echo -e "\nroot\nn\nn\nn\nn\nn" | ./usr/bin/mysql_secure_installation

# Change mysql to listen on 0.0.0.0
RUN sed -i 's/127\.0\.0\.1/0\.0\.0\.0/g' /etc/mysql/my.cnf

# Copying my-default.cnf to /usr/share/mysql
RUN cp /etc/mysql/my.cnf /usr/share/mysql/my-default.cnf

# Initializing the data directory
RUN mysql_install_db

# Exposing mysql port
EXPOSE 3306

# Creating database and setting character set to utf8
RUN service mysql start && mysql -u $mysql_username -p$mysql_password -e "CREATE DATABASE $database_name DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci; SET NAMES 'utf8';"

# Creating table user
RUN service mysql start && mysql -u $mysql_username -p$mysql_password -e "use $database_name; create table $table_name ( ID INT Primary Key Auto_Increment, NAME VARCHAR(40) NOT NULL, EMAIL VARCHAR(40) );"

# Granting permissions for tomcat server to connect to mysql server
RUN service mysql start && mysql -u $mysql_username -p$mysql_password -e "Flush privileges; GRANT ALL ON *.* to $tomcat_user@'$tomcat_ip' IDENTIFIED BY '$tomcat_password';"

# Starting mysql
CMD ["/usr/bin/mysqld_safe"]