# Linux

## Useful commands and tips

### ssh
Do not use default `22` port
```bash
ssh user@ip -p 22222
```
### IP table
### Cron job

### PS
```bash
ps aux | grep 'ruby'
```
List process, using `grep` to filter processes
### tail
Tailing texts from file in realtime

```bash
tail -f a.log
```
`f` means following, auto append texts to console
### nohup
Simply running application in background


### df
```bash
df -h
```
Show disk usage and left, `h` means show in human readable way. Normally by MB/GB.
### free
```bash
              total        used        free      shared  buff/cache   available
Mem:        3960624      416720      270024       22252     3273880     3264060
Swap:       4104188      109688     3994500
```
Show memory usage and

### Watch
```
watch kubectl get pods
```
Continuous running the commands, watching the changes. By default it refresh the result every `2s`.

### Change timezone
```bash
TZ=Asia/Shanghai;
ln -snf /usr/share/zoneinfo/$TZ /etc/localtime
```

### Check release
```bash
cat /etc/*-release
```

### Debian check system version
```bash
cat /etc/issue

cat /etc/debian_version
```

### htop
  like top, but more

#### mosh
  auto reconnect ssh

### show last something time

```bash
last shutdown
last reboot
```

### Count files in current folder

```bash
find . -type f | wc -l
```
