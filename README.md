# Docker Volume and Port Mapping Lab Exercise

## Name
Kavindhra

## Objective
- Create Docker Volumes
- Deploy Nginx using Volume Mapping
- Verify Data Persistence
- Deploy MySQL using Volume Mapping
- Verify Database Persistence

## Scenario 1 - Nginx Volume Persistence

### Create Volume

docker volume create mydata

### Run Nginx Container

docker run -d --name nginx-container -p 8080:80 -v mydata:/usr/share/nginx/html nginx:latest

### Verify Volume

docker volume ls

### Verify Container

docker ps

### Delete Container

docker stop nginx-container
docker rm nginx-container

### Recreate Container

docker run -d --name nginx-new-container -p 9090:80 -v mydata:/usr/share/nginx/html nginx:latest

### Result

Website data persisted successfully.

---

## Scenario 2 - MySQL Volume Persistence

### Create Volume

docker volume create mysql-data

### Run MySQL

docker run -d \
--name mysql-container \
-p 3306:3306 \
-v mysql-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=redhat \
mysql:8.0

### Create Database

CREATE DATABASE companydb;

### Create Table

CREATE TABLE employees(
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50),
department VARCHAR(50)
);

### Insert Records

INSERT INTO employees(name,department)
VALUES
('John','Linux'),
('David','DevOps'),
('Sam','Cloud');

### Verify Data

SELECT * FROM employees;

### Delete Container

docker stop mysql-container
docker rm mysql-container

### Recreate Container

docker run -d \
--name mysql-new-container \
-p 3307:3306 \
-v mysql-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=redhat \
mysql:8.0

### Verify Persistence

SHOW DATABASES;
USE companydb;
SELECT * FROM employees;

### Result

Database persisted successfully after container recreation.

---

## Conclusion

Docker Volumes provide persistent storage independent of container lifecycle. Data remains available even after containers are deleted and recreated.
