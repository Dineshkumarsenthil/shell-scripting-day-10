# Shell-scripting-day-10
Collection of shell scripting exercises and examples for Day 10.

---
### File Management Script
#### Create, delete, move files
```
#!/bin/bash
touch file1.txt
echo "Created file1.txt"
mv file1.txt file2.txt
echo "Renamed file1.txt to file2.txt"
rm file2.txt
echo "Deleted file2.txt"
```
---
### User Input Script
#### Ask user for name, age, validate
```
#!/bin/bash
read name
read age
if [[ -z $name && -z $age ]]; then
echo "empty"
fi
```
---
### Menu-Driven Script
#### Multi-option menu with case
```
#!/bin/bash
echo "1) touch dk3.txt"
echo "2) mkdir dk3"
echo "3) ls"
read choice
case $choice in
  1) touch dk3.txt ;;
  2) mkdir dk3 ;;
  3) ls -l ;;
  *) echo "invalid" ;;
esac
```
---
### System Information Script
#### Output CPU/memory/disk to file
```
#!/bin/bash
echo "CPU Info:" > filedk.txt
lscpu >> filedk.txt
echo -e "\nMemory Info:" >> filedk.txt
free -h >> filedk.txt
echo -e "\nDisk Info:" >> filedk.txt
df -h >> filedk.txt
```
-cat file.txt ---> It will shows CPU,Memory,Disk info.

---
### Function Automation Script
#### Functions for repetitive actions
```
#!/bin/bash

create_file() {
  touch "$1"
  echo "Created $1"
}

create_file1() {
  touch "$1"
  echo "Created (by create_file1): $1"
}
delete_file() {
  rm "$1"
  echo "Deleted $1"
}
delete_file1() {
  rm "$1"
  echo "Deleted (by delete_file1): $1"
}

# Usage examples
create_file test.txt
delete_file test.txt
create_file1 test.txt
delete_file1 test.txt
```
----
#### System monitoring using top (ps)
```
#!/bin/bash
LOG_FILE="log.txt"
DURATION=120        # total time
INTERVAL=5          # capture every 5 sec
COUNT=$((DURATION / INTERVAL))
echo "System Monitoring Started at: $(date)" > "$LOG_FILE"
echo "--------------------------------------" >> "$LOG_FILE"
for ((i=1; i<=COUNT; i++))
do
    echo -e "\n===== Capture $i at $(date) =====" >> "$LOG_FILE"

    # Capture top 3 CPU processes (non-interactive mode)
    top -b -n 1 | head -n 10 | tail -n 3 >> "$LOG_FILE"

    # Capture ps top 3 CPU consumers
    ps aux --sort=-%cpu | head -n 4 | tail -n 3 >> "$LOG_FILE"

    sleep $INTERVAL
done
echo -e "\nMonitoring Completed at: $(date)" >> "$LOG_FILE"
```
- top -b -n 1 ---> Runs top in batch mode (non-interactive).
- ps aux --sort=-%cpu --->Sorts processes by highest CPU usage.0
- head -n 10 | tail -n 3 ---> Extracts only 3 relevant process lines.
##### Loop logic
- 120 sec / 5 sec = 24 captures.
---
