# DATABASE-MIGRATION

"COMPANY": CODTECH IT SOLUTIONS

"NAME": SHASHATH.B.S

"INTERN ID": CT08SLW

"DOMAIN": SQL

"DURATION": 4 WEEKS

"MENTOR": NEELA SANTOSH

# Database Migration: MySQL to PostgreSQL

## Overview
This repository provides a step-by-step guide to migrating a database from **MySQL** to **PostgreSQL** while ensuring data integrity. The repository includes:
- **Migration scripts** for schema and data transfer.
- **Commands** to back up and restore data.
- **Documentation** on best practices for migration.

## Prerequisites
Ensure you have the following installed on your system:
- [MySQL](https://dev.mysql.com/downloads/)
- [PostgreSQL](https://www.postgresql.org/download/)

## Step 1: Export Data from MySQL
First, create a dump of your MySQL database.
```bash
mysqldump -u root -p --compatible=postgresql --no-create-info mydb > data.sql
```
This command exports only the data, without table structures.

## Step 2: Export Schema from MySQL
```bash
mysqldump -u root -p --no-data mydb > schema.sql
```
Modify `schema.sql` to replace MySQL-specific syntax:
- `AUTO_INCREMENT` → `SERIAL`
- `ENGINE=InnoDB` → Remove

## Step 3: Create Tables in PostgreSQL
After modifications, import the schema into PostgreSQL:
```bash
psql -U postgres -d mydb -f schema.sql
```

## Step 4: Import Data into PostgreSQL
```bash
psql -U postgres -d mydb -f data.sql
```
Verify the migration:
```sql
SELECT COUNT(*) FROM mytable;
```
