# 开发工具记录

## Git

提交规范，使用: [Gitflow Worklfow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

git rebase使用讨论，请参考: [https://segmentfault.com/q/1010000000430041](https://segmentfault.com/q/1010000000430041)

常用场景:

 - 查看某个文件的历史提交记录: `git log -- <file-path>`
 - 查看某个关键字的历史提交: `git log -S"keyword"` 或`git log -G"<regex>"`


## 语言

### 1. Go

常用工具 &  库:

- 日志: [logrus](https://github.com/Sirupsen/logrus)

### 2. Python

常用工具 &  库:

- [pipenv](https://github.com/pypa/pipenv)
- [requests](https://github.com/requests/requests)


## 系统排查

- [ ] sysdig
- [ ] strace - discover system calls and signals to a process
- [ ] top/htop - real time process monitoring
- [ ] netstat - network connections monitoring
- [ ] lsof - view which files are opened by which process
- [ ] tcpdump - raw network traffic monitoring
- [ ] iftop - real time network bandwidth monitoring
- [ ] vmstat - virtual memory statistics
- [ ] iotop -  Monitor Linux Disk I/O
- [ ] iostat - Input/Output Statistics
- [ ] slabtop
- [ ] systemtap
- [ ] orgalorg: ``cat /etc/hosts | fgrep terminus | awk '{print $1}' | orgalorg -s -c 2000 -j 5000 -z 5000 -a 3000 -y -t -w -d 38 -C sar -q`
- [ ] oom-killer

### 内存相关

- [ ] /proc/buddyinfo
- [ ] /proc/meminfo(Mlocked/Unevictable)
- [ ] /proc/pagetypeinfo
- [ ] /proc/sys/vm/extfrag_threshold
- [ ] /proc/sys/vm/drop_caches
- [ ] /sys/kernel/debug/extfrag/extfrag_index


1. 内存分配失败

错误信息:

```
2018-09-25 17:59:15nsenter: failed to unshare namespaces: Cannot allocate memory
2018-09-25 17:59:15container_linux.go:262: starting container process caused "process_linux.go:247: running exec setns process for init caused \"exit status 34\""
2018-09-25 17:59:15oci runtime error: container_linux.go:262: starting container process caused "process_linux.go:247: running exec setns process for init caused \"exit status 34\""
```
详情参考:

- https://blog.csdn.net/wqhlmark64/article/details/79143975
- https://www.lijiaocn.com/%E9%97%AE%E9%A2%98/2017/11/13/problem-unable-create-nf-conn.html

排查方法:

```
#dmesg -T|grep “allocation failure”
#cat /proc/buddyinfo
```
