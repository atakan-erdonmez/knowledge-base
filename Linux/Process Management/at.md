The `at` command is designed for one-off tasks. Unlike `cron` or `systemd timers`, which are for recurring tasks, `at` queues a job to be executed exactly once at a specified time.

```
at 22:00
at> <command here>
^D
```

atq -> list jobs
at -l -> list jobs

at -c <job_number> -> the job detail