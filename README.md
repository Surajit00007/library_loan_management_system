# Library Loan Management System

A complete console-based Java JDBC mini project that manages library members, books, loan transactions, returns, and overdue-book reporting.

## Features

- **Database:** Embedded Apache Derby database with normalized tables (`Members`, `Books`, and `Loans`).
- **Core Operations:** Add/view members and books, process loans, and handle book returns.
- **Transaction Safety:** Explicit transaction handling (commit/rollback) and savepoints ensure data integrity.
- **Reporting:** View active and overdue loans.
- **Benchmarking:** Built-in performance evaluation testing insert strategies, lookup methods, and commit granularities, generating a CSV report.

## Database Design

- **Members**: `member_id` (PK), `name`, `email` (UNIQUE), `active_loans`
- **Books**: `book_id` (PK), `title`, `author`, `isbn` (UNIQUE), `available`
- **Loans**: `loan_id` (PK), `member_id` (FK), `book_id` (FK), `loan_date`, `return_date`

**Indexes:**
- `idx_books_isbn` on `Books(isbn)`
- `idx_loans_member_id` on `Loans(member_id)`
- `idx_loans_return_date` on `Loans(return_date)`

## Folder Structure

```text
2341019165_Surajit/
|
+-- lib/
|   +-- derby.jar
|   +-- derbyshared.jar
|   +-- derbytools.jar
|
+-- src/
|   +-- surajit_2341019165/
|       +-- MainApp.java
|       |
|       +-- db/
|       |   +-- ConnectionManager.java
|       |   +-- DatabaseSetup.java
|       |
|       +-- dao/
|       |   +-- MemberDAO.java
|       |   +-- BookDAO.java
|       |   +-- LoanDAO.java
|       |
|       +-- model/
|       |   +-- Member.java
|       |   +-- Book.java
|       |   +-- Loan.java
|       |
|       +-- service/
|       |   +-- LibraryService.java
|       |   +-- TransactionService.java
|       |   +-- PerformanceEvaluator.java
|       |
|       +-- util/
|           +-- BenchmarkUtil.java
|           +-- ReportGenerator.java
|
+-- README.md
+-- performance_report.csv
+-- analysis_report.md
```

## How to Use

### 1. Build Instructions

Open PowerShell in the project folder and compile the source files:

```powershell
New-Item -ItemType Directory -Force -Path out
$sources = Get-ChildItem -Recurse -Filter *.java src | ForEach-Object { $_.FullName }
javac -d out $sources
```

### 2. Run Instructions

Run the console application using the required Derby jars:

**Windows:**
```powershell
java -cp "out;lib/*" surajit_2341019165.MainApp
```

**Linux / macOS:**
```bash
java -cp "out:lib/*" surajit_2341019165.MainApp
```

*(The first run will automatically create the `libraryDB` database directory.)*

### 3. Automated Self-Test

You can run an automated test that initializes the database, adds sample data, demonstrates a transaction rollback, and generates the benchmark report:

```powershell
java -cp "out;lib/*" surajit_2341019165.MainApp --self-test
```
