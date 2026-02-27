# University Management System – Database Project

## Overview

This project presents the design and implementation of a University Management System developed for a Database Management Systems course.

The system manages:

- Students
- Instructors
- Departments
- Courses
- Enrollments
- Academic performance records
- Administrative operations

It covers full database lifecycle development including:

- ER design
- Relational schema mapping
- Normalization
- PostgreSQL implementation
- Constraints and triggers
- Transaction management
- Concurrency testing
- Large-scale data validation


## Technologies Used

Database:
PostgreSQL

Backend:
Python
psycopg2

Testing:
Faker (for large data generation)

Interface:
Python-based application layer
Tailwind CSS dashboard


## Core Tables

- STUDENT
- INSTRUCTOR
- DEPARTMENT
- COURSE
- ENROLLMENT
- DEPT_LOCATION
- STUDENT_ENROLL


## Key Features

Data Integrity:
- Primary Keys
- Foreign Keys
- Unique constraints
- Check constraints
- Composite keys

Business Logic:
- Instructor retirement process
- Graduation credit check (120 credits rule)
- Department head reassignment
- Course capacity control trigger

Transactions:
All administrative operations are implemented using BEGIN / COMMIT blocks to preserve ACID properties.

Concurrency Handling:
- Row-level locking
- Race condition prevention
- Transaction abort handling (SQL State 25P02)

Scalability Testing:
- 100 Students
- 100 Instructors
- 500+ Enrollment records
- Indexed query optimization


## Reporting

The system generates:

- Student transcripts
- Department statistics
- Course enrollment summaries
- University academic summary reports


## Project Files

schema.sql
constraints.sql
triggers.sql
operations.sql
populate_db.py
outputs.sql
data.sql


## Conclusion

The system demonstrates a complete end-to-end relational database design including modeling, normalization, implementation, transaction design, concurrency control, and stress testing.

It is structurally normalized, concurrency-safe, and scalable for academic use.
