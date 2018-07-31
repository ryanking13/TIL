## rsyslog permission denied

> 실험 환경 : CentOS7

rsyslog의 configuration을 바꾸고 난 뒤 (`/etc/rsyslog.conf`, `/etc/rsyslog.d/*`)

systemd 를 이용하여 rsyslog를 실행시켰을 때, config 파일을 permission 문제로 읽어오지 못하는 문제가 발생.

1. config 파일의 permission 을 777로 주어도 해결되지 않음
1. systemd가 사용하는 rsyslog.service의 UMask, User등의 값을 세팅해도 문제가 해결되지 않음.
1. systemd를 거치지 않고 직접 rsyslogd를 실행하면 잘 실행됨.

위 상태에서 SElinux에서 rsyslog의 파일 접근을 차단한다는 것을 발견하고 해당부분을 수정하여 해결함.

```
$ sudo setenforce 0
$ sudo service rsyslog restart
```

일시적으로 SElinux를 disable 하거나,

```
# instructing se to authorize /etc/rsyslog.d/*
$ sudo semanage fcontext -a -t syslog_conf_t "/etc/rsyslog.d/"

$ sudo restorecon -R -v /etc/rsyslog.d/

$ sudo semanage fcontext -a -t etc_t "/etc/rsyslog.d"

$ sudo restorecon -v /etc/rsyslog.d
```

예외를 설정한다.

### Reference

> https://support.logz.io/hc/en-us/articles/209486429-Troubleshooting-Rsyslog-SELinux-configuration
> https://docs.logtrust.com/confluence/docs/system-configuration/sending-the-data/sending-from-unix-based-operating-systems/syslog-selinux-configuration