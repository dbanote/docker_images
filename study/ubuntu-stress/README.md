# 学习build一个运行stress命令的images

stress是一个linux下的压力测试工具，专门为那些想要测试自己的系统，完全高负荷和监督这些设备运行的用户。
参考：[Linux压力测试软件Stress安装及使用指南](https://www.cnblogs.com/jingmu/p/7645548.html)

Dockerfile
```
FROM ubuntu
RUN apt update && apt -y install stress

ENTRYPOINT ["/usr/bin/stress"]
CMD []
```

docker build -t study/ubuntu-stress .

docker run -it study/ubuntu-stress
```
`stress' imposes certain types of compute stress on your system

Usage: stress [OPTION [ARG]] ...
 -?, --help         show this help statement
     --version      show version statement
 -v, --verbose      be verbose
 -q, --quiet        be quiet
 -n, --dry-run      show what would have been done
 -t, --timeout N    timeout after N seconds
     --backoff N    wait factor of N microseconds before work starts
 -c, --cpu N        spawn N workers spinning on sqrt()
 -i, --io N         spawn N workers spinning on sync()
 -m, --vm N         spawn N workers spinning on malloc()/free()
     --vm-bytes B   malloc B bytes per vm worker (default is 256MB)
     --vm-stride B  touch a byte every B bytes (default is 4096)
     --vm-hang N    sleep N secs before free (default none, 0 is inf)
     --vm-keep      redirty memory instead of freeing and reallocating
 -d, --hdd N        spawn N workers spinning on write()/unlink()
     --hdd-bytes B  write B bytes per hdd worker (default is 1GB)

Example: stress --cpu 8 --io 4 --vm 2 --vm-bytes 128M --timeout 10s

Note: Numbers may be suffixed with s,m,h,d,y (time) or B,K,M,G (size).
```

docker run -it study/ubuntu-stress --vm 1 --verbose
```
docker run -it study/ubuntu-stress --vm 1 --verbose
stress: info: [1] dispatching hogs: 0 cpu, 0 io, 1 vm, 0 hdd
stress: dbug: [1] using backoff sleep of 3000us
stress: dbug: [1] --> hogvm worker 1 [8] forked
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
stress: dbug: [8] freed 268435456 bytes
stress: dbug: [8] allocating 268435456 bytes ...
stress: dbug: [8] touching bytes in strides of 4096 bytes ...
^Cstress: FAIL: [1] (415) <-- worker 8 got signal 2
stress: WARN: [1] (417) now reaping child worker processes
stress: FAIL: [1] (421) kill error: No such process
stress: FAIL: [1] (451) failed run completed in 1s
```