# MySQL-using-Docker
 
# MySQL Using Docker 🐳

## Overview  
This project demonstrates how to run a MySQL database using Docker, allowing seamless database management without local installations. The setup includes database creation, table structure, and initial data population.

## 📚 Documentation & Prerequisites  
Ensure you have the following installed before proceeding:  
- [Docker](https://www.docker.com/)  
- [Docker Desktop](https://www.docker.com/products/docker-desktop)  
- MySQL (Docker Image)

## 📌 Installation & Setup  

### 1️⃣ Create the Database Schema
First, create a `.sql` file (`database_students.sql`) with the following SQL commands:  
```sql
CREATE DATABASE student;
USE student;

CREATE TABLE students (
    StudentID INT NOT NULL AUTO_INCREMENT,
    FirstName VARCHAR(100) NOT NULL, 
    Surname VARCHAR(100) NOT NULL, 
    PRIMARY KEY (StudentID)
);

INSERT INTO students (FirstName, Surname)
VALUES 
    ("John", "Andersen"), 
    ("Emma", "Smith");
```

### **2️⃣ Create the Dockerfile**  
Next, create a `Dockerfile` to set up the MySQL database using Docker:  
```dockerfile
FROM mysql:latest

ENV MYSQL_ROOT_PASSWORD=root

COPY ./database_students.sql /docker-entrypoint-initdb.d/
```

## 🚀 Deployment  

### **1️⃣ Verify Docker Installation**  
Check if Docker is running by executing:  
```sh
docker container ls
```

### **2️⃣ Build the Docker Image**  
Create the Docker image for MySQL using:  
```sh
docker build -t mysql_db .
```

### **3️⃣ Verify Image Creation**  
List available Docker images:  
```sh
docker images
```

### **4️⃣ Run the MySQL Container**  
Start the MySQL database container:  
```sh
docker run --name mysql_container -d mysql_db
```

### **5️⃣ Access the Running Container**  
Enter the running container’s shell:  
```sh
docker exec -it mysql_container /bin/bash
```

### **6️⃣ Access MySQL Database**  
Once inside the container, enter MySQL and verify the student data:  
```sh
mysql -u root -p
# Enter password (default: root)
USE student;
SELECT * FROM students;
```

## 🏆 Conclusion  
You have successfully deployed a MySQL database using Docker! 🎉  
This setup ensures **portability, easy replication, and minimal local environment dependencies**.
