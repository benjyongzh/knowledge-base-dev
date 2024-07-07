# Introduction

# Installation
# How To Use
- `crontab -e` starts editing of crontab file using a text-based editor (like [[Vim]]).
- [crontab commands](https://www.hostbillo.com/blog/how-to-display-list-and-view-current-cron-jobs-in-linux/)
## Formatting
Crontabs need to follow a specific format for specifying the schedule of the script running. It comes in the form of 5 numbers `* * * * *` where each number denotes a minute/hour/day etc to run the script:

```
<minute-of-hour> <hour-of-day> <day-of-month> <month-of-year> <day-of-week>
```
### Schedule Meaning
`10 12 4 6 *` means 'run every 1210 hrs on the 4th of June'
`5 19 * 10 5` means 'run every 1905 hrs on Fridays on October'
`30 9 * * 1` means 'run every 0930 hrs on Mondays'

Other forms of flexibility in schedule are possible. `-`, `/` and `,` can be used to specify multiple values of numbers.
### Script
After specifying the schedule, the task itself has to be specified:
```
* * * * * <script>
```
where 'script' can be something like:
```
/usr/bin/python3 /home/admin/my-project/main.py
```
This tells the shell to use `python3` to run `main.py` every minute.

### Syntax Mechanics
The script itself has to mention its exact location (for e.g. /home/admin/my-project). Any outputs are relative to the `~` location.

For a situation where `~` is `/home/admin`, the following cronjob runs `main.py` and saves the output into `/home/admin/my-folder/my-file.txt`:
```
/usr/bin/python3 /home/admin/my-project/main.py > my-folder/my-file.txt
```
This means that it is important to understand where your script is and where you would want any outputs to be placed.
### Resources
- [Formatter](https://crontab.guru/)