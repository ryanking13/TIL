# Centos xfs file system corruption

```
XFS: Internal error XFS_WANT_CORRUPTED_GOTO at line 1757 of file fs/xfs/xfs_alloc.c.
...
Corruption of in-memory data detected. Shutting down filesystem
Please unmount the filesystem and rectify the problem(s)
Failed to recover EFIs
task mount:365 blocked for more than 120 seconds.
```

CentOS 부팅 과정에서 위 문제가 발생했을 떄,

```
xfs_repair -L /dev/mapper/centos-root
```

`xfs_repair`를 실행하여 문제 해소 가능

---

## Reference

> https://jc-lan.tk/2016/11/13/centos-7-fails-to-boot-xfs-corruption-enters-emergency-mode/