# scheme db-university

## Entities

- departments (primary)
- degree_courses
- courses
- professors
- exam_rounds
- students
- grades

### departments (primary)

- id (PK) BIGINT PRIMARY KEY AUTO_INCREMENT NOTNULL UNIQUE
- name VARCHAR(100) NOTNULL

### degree_courses

- id (PK) BIGINT PRIMARY KEY AUTO_INCREMENT NOTNULL UNIQUE
- name VARCHAR(100) NOTNULL
- department_id (FK) 

### courses

- id (PK) BIGINT PRIMARY KEY AUTO_INCREMENT NOTNULL UNIQUE
- name VARCHAR(100) NOTNULL 
- degree_id (FK) 

### professors

- id (PK) BIGINT PRIMARY KEY AUTO_INCREMENT NOTNULL UNIQUE
- first_name VARCHAR(50) NOTNULL
- middle_name VARCHAR(50) NULL
- last_name VARCHAR(50) NOTNULL
- email VARCHAR(100) NOTNULL UNIQUE

### pivot: course_professor

- course_id INT NOTNULL 
- professor_id INT NOTNULL 

### exam_rounds

- id (PK) BIGINT PRIMARY KEY AUTO_INCREMENT NOTNULL UNIQUE
- exam_round_id INT NOTNULL
- date DATETIME NOTNULL
- session VARCHAR(100) NOTNULL
- course_id (FK) 

### students

- id (PK) BIGINT PRIMARY KEY AUTO_INCREMENT NOTNULL UNIQUE
- first_name VARCHAR(50) NOTNULL
- middle_name VARCHAR(30) NULL
- last_name VARCHAR(50) NOTNULL 
- email VARCHAR(100) NOTNULL UNIQUE
- student_id INT NOTNULL 
- enrollment_y DATE NOTNULL
- degree_id (FK) 

### grades

- id (PK) BIGINT PRIMARY KEY AUTO_INCREMENT NOTNULL UNIQUE
- grade TINYINT NOTNULL
- is_passed TINYINT NULL
- exam_round_id (FK) 

### pivot: exam_rounds-grades

- exam_round_id INT NOTNULL
- grade_id INT NOTNULL

### pivot grades-students

- grade_id INT NOTNULL
- student_id INT NOTNULL