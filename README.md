# CODTECH-TASK4
NAME-SWAPNIL BALAJI YEREWAD
TASK NAME-DEMONSTRATE HOW TO BACK UP A DATABASE AND RESTORE IT IN CASE OF FAILURE.DELIVERABLE: BACKUP AND RECOVERY SCRIPTS, AND DOCUMENTATION OF THE PROCESS.
FEATURES-### Short Description

The process of backing up and restoring a database is essential for ensuring data integrity and security. Below is a demonstration using **MySQL** (though the steps can be adapted for other database systems like PostgreSQL or SQL Server). The deliverables include scripts for both backing up and restoring the database, as well as documentation to explain each step in the process.

---

### **Backup Process**

**Step 1: Create a Backup Script**

1. Open your terminal or command prompt.
2. Create a shell script (e.g., `backup_db.sh`).

#### Backup Script: `backup_db.sh`
```bash
#!/bin/bash

# Database credentials
USER="your_db_username"
PASSWORD="your_db_password"
DB_NAME="your_db_name"

# Backup destination directory
BACKUP_DIR="/path/to/backup/directory"
DATE=$(date +"%Y%m%d_%H%M%S")

# Backup file name
BACKUP_FILE="${BACKUP_DIR}/${DB_NAME}_backup_${DATE}.sql"

# Command to back up the database
mysqldump -u $USER -p$PASSWORD $DB_NAME > $BACKUP_FILE

# Print confirmation
if [ $? -eq 0 ]; then
  echo "Backup of database '$DB_NAME' completed successfully: $BACKUP_FILE"
else
  echo "Backup failed."
fi
```

**Step 2: Make the Script Executable**
```bash
chmod +x backup_db.sh
```

**Step 3: Run the Script**
```bash
./backup_db.sh
```

This script will back up your MySQL database into an SQL file with a timestamp.

---

### **Restore Process**

**Step 1: Create a Restore Script**

1. Create another shell script (e.g., `restore_db.sh`).

#### Restore Script: `restore_db.sh`
```bash
#!/bin/bash

# Database credentials
USER="your_db_username"
PASSWORD="your_db_password"
DB_NAME="your_db_name"

# Backup file to restore
BACKUP_FILE="/path/to/backup/file.sql"

# Command to restore the database
mysql -u $USER -p$PASSWORD $DB_NAME < $BACKUP_FILE

# Print confirmation
if [ $? -eq 0 ]; then
  echo "Restore of database '$DB_NAME' completed successfully from: $BACKUP_FILE"
else
  echo "Restore failed."
fi
```

**Step 2: Make the Script Executable**
```bash
chmod +x restore_db.sh
```

**Step 3: Run the Script**
```bash
./restore_db.sh
```

This script will restore your database from the specified backup file.

---

### **Documentation**

#### **Backup Process Documentation**

1. **Objective:** Ensure a safe and reliable backup of the database to prevent data loss.
2. **Pre-requisites:**
   - Access to the MySQL server and proper privileges.
   - A backup destination folder with write permissions.
   - The `mysqldump` utility must be installed.
3. **Steps:**
   - The `backup_db.sh` script dumps the entire database (`your_db_name`) into a timestamped SQL file.
   - The backup file is saved to the specified directory (`/path/to/backup/directory`).
4. **Execution:** Run the `backup_db.sh` script manually or schedule it using cron jobs for regular backups.
5. **Verification:** Check the backup file to ensure it contains the correct database information.

#### **Restore Process Documentation**

1. **Objective:** Restore a previously backed-up database in the event of a failure or data corruption.
2. **Pre-requisites:**
   - The backup file must be available.
   - Access to the MySQL server and proper privileges to restore databases.
3. **Steps:**
   - The `restore_db.sh` script reads the SQL backup file and loads it into the target database (`your_db_name`).
4. **Execution:** Run the `restore_db.sh` script with the path to the backup file.
5. **Verification:** After restoration, confirm that the data is correctly restored by checking the database content.

