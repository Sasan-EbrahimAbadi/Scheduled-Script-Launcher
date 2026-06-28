### Scheduled-Script-Launcher

# Old Version

A simple Bash script that repeatedly checks the system clock and launches a specified executable at fixed time intervals.

Overview

This script:

Records the current Unix timestamp when it starts.
2. Continuously monitors the current time.
3. Executes a target program when the scheduled execution time is reached.
4. Schedules the next execution time.
5. Repeats indefinitely until it stops manually.

_____________________________________
Initialization

START=$(date +%s)

Stores the current Unix timestamp (seconds since January 1, 1970 UTC) in the variable START.

Example:

1750785600
____________________________________
Infinite Loop

while true
do
    ...
done

The script runs continuously until manually terminated.
______________________________________
Time Check

($(date +%s))-($START)

Calculates the difference between:

Current Unix timestamp
Scheduled execution timestamp (START)

The target program is executed only when the difference is exactly zero.
_____________________________________
Program Execution

'/home/local_address/Filename'

Runs the executable located at local address:

/home/local_address/Filename

Make sure the file has execute permissions:

chmod +x /home/local_address/Filename
___________________________________
Rescheduling

START=$((START+180))

Updates the next execution time to 180 seconds (3 minutes) after the previous scheduled time. You can change this time to any numbers based on your need.

___________________________________
Limitations

High CPU Usage

The script continuously checks the time without any delay:

while true

This causes one CPU core to be heavily utilized.
________________
# Modified Version

A more efficient version would include a short sleep:

sleep 1

inside the loop.

Exact Timestamp Matching

The condition:

if (( $(date +%s) - START == 0 ))

requires an exact match to the second.

If the system is busy and misses that second, the scheduled task may never execute.

A safer condition would be:

if (( $(date +%s) >= START ))
