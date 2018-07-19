## ssh restriction

openSSH (sshd)를 사용할 경우 `/etc/sshd/sshd_config`를 수정하여 유저에 대한 제약을 걸 수 있다. ([link](https://www.ssh.com/ssh/sshd_config/))

특히 `Match` 옵션을 사용하여 특정 주소, 유저, 그룹 등에 대한 제약을 거는 것이 가능. (User, Group, Host, LocalAddress, LocalPort, and Address)

```
Match LocalAddress 192.168.1.101
        AllowUsers user1
        PasswordAuthentication no
```

`Subsystem`을 등록하여 sftp를 지원할 수 있다.

```
Subsystem sftp /usr/lib/ssh/sftp-server
# or
Subsystem sftp /user/lib/ssh/internal-sftp
```

이때 Match를 활용하여 적절한 접근제어가 가능

```
Match User sftpuser
        ChrootDirectory /home/download/
        ForceCommnad internal-sftp
```

---

```
AuthorizedKeysFile .ssh/authorized_keys
```

`AuthorizedKeysFile`에 지정된 파일을 사용하여 private key로 ssh 접속이 가능하게끔하는데, authorized_keys 파일을 수정하여 적절한 제약을 걸 수 있다. ([link](https://www.ssh.com/ssh/authorized_keys/openssh))

대표적으로 command 옵션을 추가하여 특정 명령 하나만 실행되도록 할 수 있다. (rsync 등에 활용)

이것을 응용하여 문자열 파싱 방식으로 명령어를 제어하는 것도 가능 ([link](http://at.magma-soft.at/sw/blog/posts/The_Only_Way_For_SSH_Forced_Commands/#thegrownuponly))