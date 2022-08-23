
## List User's Jobs
crontab -l


## Backup Users jobs by saving from this directory:
/var/spool/cron
ls /var/at/spool 


## Example cron Job (hello.py = print('hello world') ) THIS WONT PRINT WITHOUT BEING ATTACHED TO TEMRINAL, BETTER OF SENDING SHELL SCRIPT
* * * * * python /Users/ethan.knights/Desktop/work/code/python-api/cron/hello.py >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut.log

## Better example
* * * * * bash /Users/ethan.knights/Desktop/work/code/python-api/cron/job-RangeReview_freq-monthly.sh >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut_`date +%Y.%m.%d.%H.%M.%S`.log 2>&1



* * * * * bash /Users/ethan.knights/Desktop/work/code/python-api/cron/job-RangeReview_freq-monthly.sh >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut.log 2>&1

* * * * * bash /Users/ethan.knights/Desktop/work/code/python-api/cron/job-RangeReview_freq-monthly.sh >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut.log

## Error: Operation not permitted

See Udhy's SO answer:
https://apple.stackexchange.com/questions/374281/cron-lacks-permissions-to-run-a-script 
This isn't quite right, but see nohilside's comment:
Effectively, enable /usr/sbin/cron to have full disk access in SystemPreferences>Security&Privacy>Privacy. (use open /usr/sbin and drag cron for ease).
