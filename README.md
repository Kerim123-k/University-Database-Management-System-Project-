University Management System – Database Project
Overview

This project presents the design, implementation, and validation of a University Management System developed as part of the SENG301 (Database Management Systems) course.

The system is designed to manage academic and administrative data in a structured, scalable, and integrity-preserving manner. It supports core university operations such as:

Student management

Instructor management

Department administration

Course offerings

Enrollment and grading

Academic reporting

Administrative transactions

The project covers full database lifecycle development, including:

Conceptual design (ER modeling)

Relational schema mapping

Normalization (up to 3NF / BCNF where required)

PostgreSQL implementation

Business logic via constraints and triggers

Transaction design

Concurrency handling

Large-scale data testing

System Architecture
Database Management System

PostgreSQL

Backend / Integration

Python

psycopg2 for database connectivity

Faker library for large-scale test data generation

Interface

Python-based application layer

Tailwind CSS dashboard for administrative operations

Core Entities

The system is built around the following main entities:

Student

Instructor

Department

Course

Enrollment

Dept_Location (for multivalued department locations)

Student_Enroll (associative structure)

Key Relationships

A student belongs to one department.

A student has one academic advisor (instructor).

A department has one head instructor.

A department offers multiple courses.

An instructor teaches multiple courses.

Students enroll in courses (many-to-many relationship).

Enrollment stores academic performance data (grades, attendance, averages).

Database Design
Conceptual Design

Entity-Relationship Diagrams (ERD)

Clear identification of:

Strong entities

Weak entities

1:1, 1:N, and N:M relationships

Multivalued attributes

Relational Mapping

The ER model was mapped into 7 relational tables following structured transformation steps.

Normalization

Each table was analyzed for:

1NF (Atomicity)

2NF (No partial dependency)

3NF (No transitive dependency)

BCNF (Superkey determinant condition)

Most tables satisfy BCNF, while selected tables are intentionally kept in 2NF as a justified denormalization decision for performance and simplicity without introducing redundancy.

Data Integrity & Constraints

The system enforces integrity using:

Primary Keys

Foreign Keys

UNIQUE constraints

CHECK constraints

Composite keys

Domain restrictions

Row-level locking

Triggers

Examples

Course credits must be between 0 and 10.

Year level restricted to: Prep, 1, 2, 3, 4.

Enrollment prevents duplicate course registration.

Referential integrity prevents orphan records.

Trigger prevents course over-capacity.

Business Logic & Administrative Operations

Complex operations are implemented using transactional blocks (BEGIN / COMMIT) to ensure ACID compliance.

1. Instructor Retirement

Marks instructor as Retired

Reassigns courses

Reassigns student advisors

Preserves academic continuity

2. Graduation Logic

Finalizes grades

Updates earned credits

Automatically marks student as Graduated if credits ≥ 120

Removes advisor assignment

3. Department Leadership Change

Updates department head

Adjusts instructor title accordingly

All operations are atomic and rollback-safe.

Academic Reporting

The system generates dynamic reports such as:

Student List by Department

Course Enrollment Summary

Student Transcript (with photo support via BYTEA)

Department Enrollment Statistics

University Academic Summary

Reports combine multiple relational joins to transform raw data into meaningful administrative outputs.

Concurrency & Transaction Management

The system was tested under:

Multi-user concurrency

Race conditions

Simultaneous enrollment attempts

Concurrent instructor updates

Stress scenarios with multiple sessions

Concurrency Handling

Row-level locking

Exclusive and shared locks

Prevention of dirty reads

Transaction abort handling (SQL State 25P02)

Atomic and isolated operations

PostgreSQL successfully maintained ACID properties under stress testing.

Scalability Testing

To simulate real-world load:

100 student records inserted

100 instructor records inserted

500+ enrollment records inserted

Optimizations

B-tree indexes on:

Student_ID

Course_ID

Trigger validation tested under large datasets

Query performance validated under heavy load

The system maintained consistency and performance integrity.

Project Structure
schema.sql          # Full DDL schema
constraints.sql     # Domain and integrity constraints
triggers.sql        # Business logic triggers
operations.sql      # Transactional administrative operations
populate_db.py      # Large-scale data generator (Faker)
outputs.sql         # Report query outputs
data.sql            # Sample data
Testing Methodology

The system was validated through three phases:

Phase 1 – Constraint Testing

Duplicate primary key rejection

Invalid grade rejection

Foreign key enforcement

Phase 2 – Concurrent Operations

Race condition simulation

Capacity enforcement

Multi-admin update tests

Phase 3 – Large Data Validation

Stress testing

Performance validation

Business logic verification on populated database

Design Principles Applied

Elimination of redundancy

Avoidance of unnecessary NULL values

Prevention of invalid tuples

Referential integrity preservation

Justified denormalization where beneficial

ACID-compliant transaction management

Learning Outcomes

This project provided hands-on experience in:

Thinking like a database designer

Entity identification and modeling

Functional dependency analysis

Normalization and denormalization trade-offs

Transaction design

Concurrency handling

Real DBMS implementation

Bridging conceptual design to production-level system

References

The following sources were reviewed for general understanding of university database structures:

University Database Project (GitHub)

Baeldung – Full SQL Schema Examples

No direct code or schema was copied; references were used only for conceptual orientation.

Conclusion

The University Management System demonstrates a complete end-to-end database design and implementation process, from conceptual modeling to real-world stress testing.

The final system is:

Structurally normalized

Semantically correct

Concurrency-safe

Scalable

ACID-compliant

Suitable for real academic environments
