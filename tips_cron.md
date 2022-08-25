
## List User's Jobs
```
crontab -l
```

## Backup Users jobs by saving from this directory:
```
/var/spool/cron
ls /var/at/spool 
```


## Better example (run every minute)
```sh
* * * * * bash /Users/ethan.knights/Desktop/work/code/python-api/cron/job-RangeReview_freq-monthly.sh >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut_`date +%Y.%m.%d.%H.%M.%S`.log 2>&1
```



```sh
* * * * * bash /Users/ethan.knights/Desktop/work/code/python-api/cron/job-RangeReview_freq-monthly.sh >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut.log 2>&1
```

```sh
* * * * * bash /Users/ethan.knights/Desktop/work/code/python-api/cron/job-RangeReview_freq-monthly.sh >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut.log
```

## Example job (every minute append output to file)
```sh
crontab -e #edit
crontab -l #check job passes cron checks
```
 Contents of crontab:
```sh
* * * * * bash /Users/ethan.knights/Desktop/work/code/python-api/cron/job-RangeReview_freq-monthly.sh >> /Users/ethan.knights/Desktop/work/code/logs_cron/rangeReview/cronOut_`date +\%Y-\%m-\%d_\%H:\%M:\%S`.log 2>&1
```



Contents of the job: job-RangeReview_freq-monthly.sh
```sh
#!/bin/bash
/opt/homebrew/anaconda3/bin/python /Users/ethan.knights/Desktop/work/code/python-api/cron/hello.py

echo 'successfully ran python above'
#echo 'Hello World' > /home/myname/script1.sh.out 2>&1
```


## Delete old crontab jobs
```sh
crontab -r
```


## Error: Operation not permitted
See Udhy's SO answer:
https://apple.stackexchange.com/questions/374281/cron-lacks-permissions-to-run-a-script 
This isn't quite right, but see nohilside's comment:
Effectively, enable /usr/sbin/cron to have full disk access in SystemPreferences>Security&Privacy>Privacy. (use open /usr/sbin and drag cron for ease).
