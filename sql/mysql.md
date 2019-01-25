# mysql

## mysql远程授权访问
- GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' with GRANT OPTION;
- flush privileges;

## 创建数据库
- DROP DATABASE IF EXISTS `my_db`;
- CREATE DATABASE `my_db` CHARACTER SET 'utf8' COLLATE 'utf8_general_ci';
- USE `my_db`;