# CPU
4 critical performance metrics:
- Context switch
- Run queue
- CPU utilization
- Load average

## Context Switch
When CPU switches from one process/thread to another, it is called "context switch"
Context switch time: The time it takes to context switch

You can see the context switch count via:
`/proc/<pid>/status`

![[CPU_Context_Switch.png]]
Voluntary: Kernel schedule
Involuntary: Interruption

## Run Queue
The queue that CPU will run. It will decide based on priority, nice number.
The run queue indicates the total number of active processes in your current queue for CPU.
## CPU Utilization
Means how much CPU is used

## Load average
It indicates the average CPU load over a specific time period.

It is written as "0.75 1.70 2.10", which means the last 1min, last 5min, and last 15min.

- It is calculated by combining the run queue and uninterruptable tasks.

```
uptime
# For load average (?)
```

# IO
- I/O wait is the amount o time CPU is waiting for I/O. If you see consistent high I/O wait, it indicates a problem on the disk subsystem

- You should also monitor reads/second and writes/second. This is measured in blocks

- tps indicates total transactions per second, which is sum of rtps (read rts) and wtps (write rts)


# Memory

Page: The memory is divided into chunks, which are called pages.

swapper: The process that makes swap-in swap-out

# Basic Programs
- top
- vmstat
- iostat
- free
- sar
-

## Top
### %cpu sections:
us: user process
sy: system process
ni: priority 
id: idle (not used)
wa: I/O operation wait (high=bad)
hi: Hardware interrupts
si: Software interrupts 
st: Stolen from hypervisor

### mem sections:
Free: Free memory + buff/cache
Buff/cache: buffer and cache memory

### Process section
[[PS & Top]]

PR: Priority
NI: Nice
VIRT: Virtual memory
RES: Physical memory
SHR: Shared memory
S: State
TIME: Total timefo
PPID: Parent PID
C: CPU
STIME: Start time

## Vmstat
`vmstat 10` -> update every 10 sec

- r: Programs in run queue, waiting for CPU
- b: I/O wait queue
- swpd: How many swap blocks/pages is used
- si: swap in
- so: swap out
- bi: Blocks in (read)
- bo: Blocks out (write
- in: Interrupts
- cs: Context switch per second

- CPU part is same in TOP 