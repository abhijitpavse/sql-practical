# 🏥 Hospital Management System — MySQL

![MySQL](https://img.shields.io/badge/Database-MySQL-blue)
![SQL](https://img.shields.io/badge/Language-SQL-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

A scenario-based **Hospital Management System** developed using **MySQL** to demonstrate relational database design, SQL programming, stored procedures, stored functions, triggers, transaction management, exception handling, error logging, billing, payments, room allocation, and complete patient workflow management.

The project is designed around a fictional **CarePlus Hospital** and implements an end-to-end patient workflow, from patient registration and appointment booking to admission, room allocation, billing, payment, and discharge.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Objectives](#-objectives)
- [Hospital Scenario](#-hospital-scenario)
- [Database Architecture](#-database-architecture)
- [Database Entities](#-database-entities)
- [Key Relationships](#-key-relationships)
- [Technologies Used](#-technologies-used)
- [Project Structure](#-project-structure)
- [SQL Features Implemented](#-sql-features-implemented)
- [Variables and Operators](#-variables-and-operators)
- [Conditional Logic](#-conditional-logic)
- [Loops](#-loops)
- [Stored Procedures](#-stored-procedures)
- [Stored Functions](#-stored-functions)
- [Triggers](#-triggers)
- [Billing and Payment Workflow](#-billing-and-payment-workflow)
- [Transaction Control](#-transaction-control)
- [Exception Handling](#-exception-handling)
- [Error Logging](#-error-logging)
- [Required Test Cases](#-required-test-cases)
- [Rahul Sharma Integrated Workflow](#-rahul-sharma-integrated-workflow)
- [Final Output](#-final-output)
- [Expected Final Output](#-expected-final-output)
- [Submission Requirements](#-submission-requirements)
- [How to Run](#-how-to-run)
- [Learning Outcomes](#-learning-outcomes)
- [Submission Checklist](#-submission-checklist)
- [Project Highlights](#-project-highlights)
- [Author](#-author)

---

# 📖 Project Overview

The **Hospital Management System** is a relational database project created to manage core hospital operations using MySQL.

The system handles:

- Patient registration
- Department management
- Doctor management
- Appointment booking
- Room allocation
- Patient admissions
- Billing
- Payments
- Patient discharge
- Error logging
- Transaction management

The project goes beyond basic CRUD operations by implementing **MySQL programming features** to enforce hospital-specific business rules and automate dependent database operations.

It demonstrates how SQL can be used to solve practical business problems rather than simply creating isolated SQL examples.

---

# 🎯 Objectives

The main objectives of this project are to:

- Design a relational hospital database.
- Create appropriate tables, primary keys, and foreign keys.
- Insert realistic hospital sample data.
- Apply constraints to prevent invalid data.
- Use variables and SQL operators for calculations and conditions.
- Implement conditional logic using `IF`, `ELSEIF`, and `ELSE`.
- Implement loops for repetitive hospital operations.
- Develop reusable stored procedures.
- Develop reusable stored functions.
- Automate database updates using triggers.
- Demonstrate `COMMIT`, `ROLLBACK`, `SAVEPOINT`, and `RELEASE SAVEPOINT`.
- Implement exception handling using MySQL handlers.
- Use `SIGNAL` for business-rule validation.
- Use `GET DIAGNOSTICS` to capture SQL error information.
- Maintain an `Error_Log` table for failed operations.
- Test valid and invalid hospital operations.
- Demonstrate a complete patient workflow using Rahul Sharma.

---

# 🏥 Hospital Scenario

The project is based on a fictional hospital named **CarePlus Hospital**.

The hospital requires a database system to manage:

- Patients
- Departments
- Doctors
- Appointments
- Rooms
- Admissions
- Bills
- Payments
- Errors

The system also prevents invalid operations. Examples include:

- A patient cannot be registered with a duplicate phone number.
- An appointment cannot be booked for a non-existing patient.
- An appointment cannot be booked for a non-existing doctor.
- An occupied room cannot be allocated again.
- A payment cannot exceed the outstanding bill amount.
- Invalid business operations generate controlled errors.
- Successful payments automatically update bill payment status.
- Patient discharge automatically makes the assigned room available.
- Errors generated during procedure execution are recorded in `Error_Log`.

---

# 🗄️ Database Architecture

The database used in this project is:

```text
HospitalManagementDB
```

The database contains the following main entities:

```text
Departments
Patients
Doctors
Appointments
Rooms
Admissions
Bills
Payments
Error_Log
```

The database follows a relational structure using:

- Primary Keys
- Foreign Keys
- Unique Constraints
- Not Null Constraints
- Check Constraints
- Default Values
- Relationships between entities

---

# 📊 Database Entities

### 1. Departments

Stores hospital department information.

Examples: Cardiology, Emergency, Pediatrics, General Medicine.

Main information: Department ID, Department Name, Location, Creation Date.

### 2. Patients

Stores patient information.

Main information: Patient ID, First Name, Last Name, Date of Birth, Gender, Phone, Email, Address, Patient Condition, Registration Date.

The table uses constraints to prevent duplicate contact information and invalid data.

### 3. Doctors

Stores doctor information.

Main information: Doctor ID, Doctor Name, Specialization, Department, Phone, Consultation Fee.

Doctors are linked to departments using a foreign key.

### 4. Appointments

Manages patient appointments.

Main information: Appointment ID, Patient ID, Doctor ID, Appointment Date, Appointment Type, Priority, Status, Notes, Creation Date.

- **Appointment types:** Regular, Emergency, Follow-up
- **Appointment status:** Scheduled, Completed, Cancelled

### 5. Rooms

Manages hospital rooms.

Main information: Room ID, Room Number, Room Type, Daily Charge, Availability.

- **Room types:** General, Semi-Private, Private, ICU
- **Availability:** Available, Occupied

### 6. Admissions

Manages inpatient admissions.

Main information: Admission ID, Patient ID, Room ID, Admission Date, Discharge Date, Diagnosis, Admission Status.

- **Admission status:** Admitted, Discharged

### 7. Bills

Manages patient billing.

Main information: Bill ID, Patient ID, Admission ID, Consultation Charge, Room Charge, Medicine Charge, Other Charge, Subtotal, Discount, Tax, Total Amount, Payment Status, Bill Date.

- **Payment status:** Pending, Partially Paid, Paid

### 8. Payments

Stores payment transactions.

Main information: Payment ID, Bill ID, Payment Date, Amount, Payment Method, Payment Status.

- **Payment methods:** Cash, Card, UPI, Online
- **Payment status:** Successful, Failed

### 9. Error_Log

Stores errors generated during stored procedure execution.

It records: Error ID, Error Time, Procedure Name, Error Message, Related Identifier.

This provides a centralized mechanism for tracking failed operations.

---

# 🔗 Key Relationships

The database uses primary keys and foreign keys to establish relationships between entities.

```text
                 Departments
                      │
                      ▼
                   Doctors
                      │
                      ▼
                 Appointments
                      ▲
                      │
                   Patients
                    │   │
          ┌─────────┘   └──────────┐
          ▼                        ▼
     Admissions                   Bills
          │                        │
          ▼                        ▼
        Rooms                   Payments
```

### Main Relationships

| Parent | Child |
|--------|-------|
| Departments | Doctors |
| Patients | Appointments |
| Doctors | Appointments |
| Patients | Admissions |
| Rooms | Admissions |
| Patients | Bills |
| Admissions | Bills |
| Bills | Payments |

---

# 🛠️ Technologies Used

| Category | Tool |
|----------|------|
| Database | MySQL |
| Language | SQL |
| Database Client | MySQL Workbench |
| Version Control | Git |
| Repository Hosting | GitHub |

---

# 📁 Project Structure

The project is organized into separate SQL files according to the different sections and requirements.

```text
Hospital-Management-System/
│
├── README.md
│
├── 01_Database_and_Tables.sql
├── 02_Sample_Data.sql
├── 03_Variables_and_Operators.sql
├── 04_IF_ELSE_Decisions.sql
├── 05_Loops.sql
├── 06_Stored_Procedures.sql
├── 07_Stored_Functions.sql
├── 08_Triggers.sql
├── 09_Transactions_TCL.sql
├── 10_Exception_Handling.sql
├── 11_Required_Test_Cases.sql
└── 12_Final_Rahul_Workflow.sql
```

### File Description

| File | Description |
|------|-------------|
| `01_Database_and_Tables.sql` | Creates the database and all required tables |
| `02_Sample_Data.sql` | Inserts realistic hospital sample data |
| `03_Variables_and_Operators.sql` | Demonstrates variables and SQL operators |
| `04_IF_ELSE_Decisions.sql` | Implements hospital decision-making using conditional logic |
| `05_Loops.sql` | Implements WHILE, LOOP/CURSOR, and REPEAT operations |
| `06_Stored_Procedures.sql` | Contains hospital management stored procedures |
| `07_Stored_Functions.sql` | Contains reusable stored functions and test SELECT queries |
| `08_Triggers.sql` | Creates and tests automatic database triggers |
| `09_Transactions_TCL.sql` | Demonstrates COMMIT, ROLLBACK, SAVEPOINT, and RELEASE SAVEPOINT |
| `10_Exception_Handling.sql` | Demonstrates exception handling and Error_Log |
| `11_Required_Test_Cases.sql` | Contains the required 15 test cases |
| `12_Final_Rahul_Workflow.sql` | Demonstrates the complete Rahul Sharma hospital workflow |

---

# ⚙️ SQL Features Implemented

| Feature | Implementation |
|---------|----------------|
| Database Design | Relational Hospital Database |
| Primary Keys | Implemented |
| Foreign Keys | Implemented |
| Constraints | PK, FK, UNIQUE, NOT NULL, CHECK |
| Sample Data | Patients, doctors, departments, rooms, appointments, admissions, bills, payments |
| Variables | Session and local variables |
| Operators | Arithmetic, comparison, logical |
| Conditional Logic | IF / ELSEIF / ELSE |
| Business Validation | SIGNAL |
| Loops | WHILE, LOOP, REPEAT |
| Stored Procedures | 5+ |
| Stored Functions | 3+ |
| Triggers | 3+ |
| Transactions | COMMIT / ROLLBACK |
| Savepoints | SAVEPOINT / ROLLBACK TO SAVEPOINT / RELEASE SAVEPOINT |
| Exception Handling | SQLEXCEPTION handlers |
| Diagnostics | GET DIAGNOSTICS |
| Error Logging | Error_Log |
| Testing | 15 required test cases |
| Integrated Workflow | Rahul Sharma |

---

# 🔢 Variables and Operators

Variables are used for hospital-related calculations such as consultation charges, room charges, medicine charges, other charges, subtotal, discount, tax, and final bill amount.

### Session Variables

```sql
@consultation_fee
@room_charge
@medicine_charge
@other_charge
@tax_rate
@discount_rate
```

### Local Variables

Local variables are used inside stored procedures for temporary calculations and business-rule processing.

### Arithmetic Operators

```text
+   -   *   /
```

Used for adding charges, calculating discounts, calculating taxes, and calculating final bill amounts.

### Comparison Operators

```text
=   >   <   >=   <=   <>
```

Used for comparing payments and balances, checking patient conditions, checking room availability, and validating dates.

### Logical Operators

```text
AND   OR   NOT
```

Used to combine multiple hospital business conditions.

---

# 🔀 Conditional Logic

The project uses `IF`, `ELSEIF`, and `ELSE` to implement actual hospital decision-making.

### Patient Age Classification

```text
Age < 18       → Child
Age 18–59      → Adult
Age >= 60      → Senior
```

### Appointment Priority

Priority is determined using appointment type and patient condition.

```text
Emergency condition → Emergency Priority
Critical condition  → Emergency Priority
Serious condition   → High Priority
Follow-up           → Normal Priority
Other               → Low Priority
```

### Payment Status

```text
No successful payment → Pending
Partial payment       → Partially Paid
Full payment          → Paid
```

### Room Allocation

Room allocation checks:

- Whether the patient exists
- Whether the room exists
- Whether the room is available
- Whether the patient already has an active admission
- Whether ICU requirements are satisfied

Business-rule violations are raised using `SIGNAL SQLSTATE '45000'`.

---

# 🔁 Loops

The project implements multiple loops for repetitive hospital operations.

### 1. WHILE Loop

Used to generate appointment records for multiple days.

```text
Start Date → Day 1 Appointment → Day 2 Appointment → Day 3 Appointment → ...
```

The loop uses a counter to control the number of generated appointments.

### 2. LOOP with Cursor

Used to process unpaid bills.

```text
Read unpaid bill
      ↓
Calculate successful payments
      ↓
Calculate outstanding balance
      ↓
Classify bill
      ↓
Read next bill
      ↓
Repeat
```

### 3. REPEAT Loop

Used for repeated reminder-generation operations.

The project therefore demonstrates more than the required two loops.

---

# ⚙️ Stored Procedures

The project implements more than the required five stored procedures.

### 1. `RegisterPatient()`

Registers a new patient after validating patient information, duplicate phone number, duplicate email, and date of birth. Includes exception handling and error logging.

### 2. `BookAppointment()`

Books an appointment after checking patient existence, doctor existence, appointment date, doctor scheduling conflicts, and appointment priority.

### 3. `ProcessPayment()`

Processes patient payments and validates bill existence, positive payment amount, outstanding balance, and overpayment prevention. Also updates the bill payment status.

### 4. `GeneratePatientBill()`

Generates a patient bill using consultation charges, room charges, medicine charges, other charges, discount, tax, and final amount.

### 5. `AllocateRoom()`

Allocates an available room to an admitted patient after checking patient existence, room existence, room availability, existing admission, and ICU suitability.

---

# 🧮 Stored Functions

The project implements reusable stored functions for common hospital calculations.

### `CalculateAge()`

Calculates the patient's age from the date of birth.

```sql
SELECT CalculateAge('2000-05-15') AS Age;
```

### `GetPatientCategory()`

Classifies a patient as Child, Adult, or Senior.

```sql
SELECT GetPatientCategory('2000-05-15') AS Patient_Category;
```

### `CalculateBillBalance()`

Calculates the outstanding balance of a bill.

```sql
SELECT CalculateBillBalance(1) AS Outstanding_Balance;
```

### `CalculateLengthOfStay()`

Calculates the number of days a patient stayed in the hospital.

```sql
SELECT CalculateLengthOfStay(1) AS Length_Of_Stay;
```

Each function includes test `SELECT` statements in the corresponding SQL file.

---

# 🔔 Triggers

The project implements three major triggers to automate dependent database updates.

### 1. Payment Trigger

After a successful payment is inserted, the trigger recalculates the successful payment total and updates the bill status.

```text
Payment Inserted
       ↓
Successful Payment
       ↓
Calculate Total Paid
       ↓
Compare with Bill
       ↓
Update Bill Status (Pending / Partially Paid / Paid)
```

### 2. Admission Trigger

When a patient admission is inserted, the assigned room is automatically marked **Occupied**.

### 3. Discharge Trigger

When an admission is updated from Admitted to Discharged, the assigned room automatically becomes **Available**.

These triggers automate dependent updates and reduce manual database operations.

---

# 💳 Billing and Payment Workflow

```text
Consultation Charges
        +
Room Charges
        +
Medicine Charges
        +
Other Charges
        ↓
     Subtotal
        ↓
     Discount
        ↓
       Tax
        ↓
   Final Amount
        ↓
     Payment
        ↓
Pending / Partially Paid / Paid
```

Every payment is validated against the outstanding bill balance.

### Payment Flow

```text
Bill Generated → Pending → Partial Payment → Partially Paid
      → Remaining Payment → Paid → Outstanding Balance = 0
```

---

# 🔐 Transaction Control

The project demonstrates MySQL Transaction Control Language (TCL).

Implemented commands:

```sql
START TRANSACTION;
COMMIT;
ROLLBACK;
SAVEPOINT savepoint_name;
ROLLBACK TO SAVEPOINT savepoint_name;
RELEASE SAVEPOINT savepoint_name;
```

| Command | Purpose |
|---------|---------|
| `COMMIT` | Permanently saves successful database operations |
| `ROLLBACK` | Undoes database changes when a transaction fails |
| `SAVEPOINT` | Creates a checkpoint inside a transaction |
| `ROLLBACK TO SAVEPOINT` | Undoes only the operations performed after a savepoint, keeping earlier changes |
| `RELEASE SAVEPOINT` | Removes a savepoint when it is no longer required |

---

# 🚨 Exception Handling

Stored procedures include exception handlers using:

```sql
DECLARE EXIT HANDLER FOR SQLEXCEPTION
```

SQL error information is captured using:

```sql
GET DIAGNOSTICS CONDITION 1
```

The captured information is stored in the `Error_Log` table.

Business-rule violations are raised using:

```sql
SIGNAL SQLSTATE '45000'
```

Examples include:

- Invalid payment amount
- Payment greater than outstanding balance
- Non-existing patient
- Non-existing doctor
- Non-existing room
- Occupied room allocation
- Invalid business conditions

---

# 📝 Error Logging

The `Error_Log` table provides a centralized record of procedure failures.

Stored information: Error ID, Error Time, Procedure Name, Error Message, Related Identifier.

```text
Procedure Execution
        ↓
Error Occurs
        ↓
Exception Handler
        ↓
GET DIAGNOSTICS
        ↓
Error_Log
```

This allows failed operations to be reviewed and diagnosed.

---

# 🧪 Required Test Cases

The project includes all 15 required test cases.

| # | Test Case | Expected Result |
|---|-----------|-----------------|
| 1 | Register a new patient successfully | Patient registered |
| 2 | Attempt duplicate patient registration | Validation/error generated |
| 3 | Book a valid appointment | Appointment created |
| 4 | Book appointment for non-existing patient/doctor | Operation rejected |
| 5 | Allocate an available room | Room allocated and marked occupied |
| 6 | Attempt to allocate an occupied room | Allocation rejected |
| 7 | Generate a bill | Charges calculated correctly |
| 8 | Process a valid partial payment | Bill becomes partially paid |
| 9 | Attempt payment greater than outstanding balance | Payment rejected |
| 10 | Complete remaining payment | Bill becomes fully paid |
| 11 | Discharge patient | Room becomes available |
| 12 | Force a procedure error | Error_Log receives error |
| 13 | Execute successful transaction | COMMIT verified |
| 14 | Execute failed transaction | ROLLBACK verified |
| 15 | Use SAVEPOINT and ROLLBACK TO SAVEPOINT | Partial rollback verified |

---

# 👨‍⚕️ Rahul Sharma Integrated Workflow

The project includes a complete integrated hospital workflow using **Rahul Sharma**.

```text
Rahul Sharma
     ↓
Patient Registration
     ↓
Appointment Booking
     ↓
Doctor Consultation
     ↓
Patient Admission
     ↓
Room Allocation
     ↓
Bill Generation
     ↓
Partial Payment
     ↓
Bill = Partially Paid
     ↓
Remaining Payment
     ↓
Bill = Paid
     ↓
Patient Discharge
     ↓
Room = Available
```

### Workflow Components

- Patient registration
- Appointment booking and completion
- Patient condition update
- Room allocation and admission creation
- Bill generation and balance calculation
- Partial payment with automatic payment-status update
- Remaining payment and final bill settlement
- Patient age/category calculation
- Length-of-stay calculation
- Patient discharge with automatic room availability update
- Final workflow reporting

This scenario demonstrates how all major components of the database work together.

---

# 📊 Final Output

The final SQL queries provide reports showing the completed hospital workflow.

| Report | Details Displayed |
|--------|-------------------|
| Patient Information | Patient ID, name, date of birth, patient category, condition |
| Appointment Information | Appointment ID, doctor, date, type, priority, status |
| Admission Information | Admission ID, admission date, discharge date, diagnosis, status |
| Room Information | Room number, room type, availability |
| Billing Information | Bill ID, subtotal, discount, tax, total amount, payment status |
| Payment Information | Payment history, total paid, outstanding balance, payment status |
| Error Information | Error ID, error time, procedure name, error message, related identifier |

---

# 🎯 Expected Final Output

The completed project demonstrates the ability to design and implement a relational hospital database and use MySQL programming features to solve real business problems.

The final database:

- Prevents invalid operations where possible.
- Applies meaningful hospital business rules.
- Validates patient, doctor, room, bill, and payment information.
- Automates dependent updates using triggers.
- Calculates bills and outstanding balances.
- Manages patient admissions and room availability.
- Handles successful and failed transactions.
- Recovers safely from failures using transactions.
- Uses savepoints for partial transaction rollback.
- Records useful error information in `Error_Log`.
- Successfully executes the complete Rahul Sharma workflow.

---

# 📋 Submission Requirements

| Component | Contents |
|-----------|----------|
| Database and Tables | Database creation, table creation, primary keys, foreign keys, constraints |
| Sample Data | Departments, doctors, patients, appointments, rooms, admissions, bills, payments |
| Stored Procedures | Comments explaining parameters, local variables, conditions, loops, exception handlers, business rules |
| Stored Functions | Functions with corresponding test SELECT statements |
| Triggers | Triggers with test INSERT and UPDATE operations |
| TCL Demonstrations | COMMIT, ROLLBACK, SAVEPOINT, ROLLBACK TO SAVEPOINT, RELEASE SAVEPOINT |
| Exception Handling | Exception handlers, GET DIAGNOSTICS, SIGNAL, error logging, Error_Log output |
| Final Workflow | Final SELECT queries showing the completed hospital workflow |

---

# ▶️ How to Run

### Step 1 — Clone the Repository

```bash
git clone https://github.com/abhijitpavse/Hospital-Management-System.git
cd Hospital-Management-System
```

### Step 2 — Open MySQL Workbench

Open the project SQL files using MySQL Workbench.

### Step 3 — Create Database and Tables

Run `01_Database_and_Tables.sql`. This creates `HospitalManagementDB` and all required tables.

### Step 4 — Insert Sample Data

Run `02_Sample_Data.sql`.

### Step 5 — Execute Variables and Decision Logic

Run `03_Variables_and_Operators.sql` and `04_IF_ELSE_Decisions.sql`.

### Step 6 — Execute Loops

Run `05_Loops.sql`.

### Step 7 — Create Stored Procedures

Run `06_Stored_Procedures.sql`.

### Step 8 — Create and Test Functions

Run `07_Stored_Functions.sql`.

### Step 9 — Create and Test Triggers

Run `08_Triggers.sql`.

### Step 10 — Run Transaction Demonstrations

Run `09_Transactions_TCL.sql`.

### Step 11 — Run Exception Handling

Run `10_Exception_Handling.sql`, then verify generated errors:

```sql
SELECT * FROM Error_Log;
```

### Step 12 — Run Required Test Cases

Run `11_Required_Test_Cases.sql` to verify all 15 required test scenarios.

### Step 13 — Run Final Integrated Workflow

Run `12_Final_Rahul_Workflow.sql`.

### Step 14 — Verify Final Reports

Run the final SELECT queries to verify Patients, Doctors, Appointments, Admissions, Rooms, Bills, Payments, and Error_Log.

---

# 🎓 Learning Outcomes

Through this project, the following concepts are demonstrated:

- Relational database design
- Entity relationships
- Primary keys and foreign keys
- Database constraints
- Data validation
- SQL variables
- Arithmetic, comparison, and logical operators
- Conditional statements
- WHILE, LOOP/CURSOR, and REPEAT loops
- Stored procedures
- Stored functions
- Database triggers
- Billing calculations
- Payment validation
- Transaction management (COMMIT, ROLLBACK, SAVEPOINT, ROLLBACK TO SAVEPOINT, RELEASE SAVEPOINT)
- Exception handling (SIGNAL, GET DIAGNOSTICS)
- Error logging
- Business-rule implementation
- End-to-end database testing

---

# ✅ Submission Checklist

- [x] Database and all tables created
- [x] Sample data inserted
- [x] Variables demonstrated
- [x] Operators demonstrated
- [x] IF / ELSEIF / ELSE demonstrated
- [x] At least 2 loops implemented
- [x] At least 5 procedures implemented
- [x] At least 3 functions implemented
- [x] At least 3 triggers implemented
- [x] COMMIT demonstrated
- [x] ROLLBACK demonstrated
- [x] SAVEPOINT demonstrated
- [x] ROLLBACK TO SAVEPOINT demonstrated
- [x] RELEASE SAVEPOINT demonstrated
- [x] Exception handlers implemented
- [x] SIGNAL business validation implemented
- [x] GET DIAGNOSTICS demonstrated
- [x] Error_Log populated during an error test
- [x] 15 required test cases completed
- [x] Rahul Sharma integrated workflow tested
- [x] Final SELECT reports generated

---

# 🚀 Project Highlights

- 🏥 Real-world hospital management scenario
- 🗄️ Relational MySQL database design
- 🔗 Primary and foreign key relationships
- 🔐 Data validation and business rules
- ⚙️ 5+ stored procedures
- 🧮 3+ stored functions
- 🔔 3+ database triggers
- 🔁 Multiple SQL loops
- 💳 Automated billing and payment tracking
- 🏨 Room and admission management
- 🚨 Exception handling and error logging
- 🔄 Transaction and savepoint management
- 🧪 15 required test cases
- 👨‍⚕️ Complete Rahul Sharma patient workflow
- 📊 Final hospital workflow reports

---

# 📚 Project Documentation

This repository is organized according to the project requirements. The SQL files contain the actual implementation, while this README provides an overview of the database architecture, hospital entities, SQL programming concepts, stored procedures, functions, triggers, transactions, exception handling, error logging, test cases, integrated workflow, and project execution steps.

Sections describing expected output, submission requirements, checklist items, and instructions are documentation and evaluation criteria rather than separate SQL coding modules.

---

# 👨‍💻 Author

**Abhijit Pavse**

Computer Science Graduate | Aspiring Data Engineer

Interested in: Data Engineering • Data Analytics • SQL • Python • Databases • Artificial Intelligence

### Connect With Me

- GitHub: [github.com/abhijitpavse](https://github.com/abhijitpavse)
- LinkedIn: [linkedin.com/in/abhijitpavse](https://www.linkedin.com/in/abhijitpavse/)
- LeetCode: [leetcode.com/u/abhijitpavse](https://leetcode.com/u/abhijitpavse/)

---

## ⭐ Project Note

This project was developed as a scenario-based MySQL database project to demonstrate practical implementation of relational database concepts and MySQL programming features in a hospital management environment.

It focuses on using SQL to solve real-world hospital business problems through validation, automation, transaction management, exception handling, and integrated workflow processing.

## ⭐ If You Find This Project Useful

Feel free to explore the SQL files and review the implementation to learn more about:

**MySQL • SQL • DBMS • Stored Procedures • Stored Functions • Triggers • Transactions • Exception Handling • Database Design • Hospital Management Systems**
