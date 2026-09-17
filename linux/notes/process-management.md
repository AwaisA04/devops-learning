# process management

## commands

i started a background process using sleep 100 &

```bash
sleep 100 &
```
this gave me the PID for the process, 87063

i then used the jobs command to see all running processes, sleep was active and running

```bash
jobs
```

i then used ps aux and piped it to grep sleep to find me the contents of sleep, i could also use top or htop to get a live viewing

```bash
ps aux | grep sleep
```

now that i had the pid by using the ps aux command all i had to do was kill the process

```bash
kill 87063
```