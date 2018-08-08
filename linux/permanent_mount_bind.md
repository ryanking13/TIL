## Permanent mount bind

> 테스트 환경 : Arch linux 4.16.7


`mount --bind` 옵션을 사용하면 특정 디렉토리(파일)을 다른 디렉토리 서브트리에 붙일 수 있다.

심볼릭 링크(`ln -s`)와 다른 점은, sftp ChrootDirectory 옵션 등으로 루트 디렉토리가 변경된 경우에도 접근이 가능하다는 점.

예를 들어, sftp에 접속하는 유저가 /a/b/c/d /a/e/f/g 두 개 디렉토리를 보게 하고 싶은데,

루트 디렉토리를 /a로 설정하면 d, g외에도 다른 파일을 볼 수 있고, /a/b/c/d로 설정하고 g의 심볼릭 링크를 두는 것은 제대로 동작하지 않는데,
이때 g를 d의 서브 디렉토리에 bind하면 원하는 결과를 얻을 수 있다.

다만 mount --bind는 시스템 리부팅시에 삭제되므로, permanent하게 bind된 상태로 남기고 싶다면,

`/etc/fstab`에 아래 줄을 추가해야 한다.

/src/path   /dst/path   none    bind,ro 0 0

findmnt, mount 명령어 등으로는 제대로 된 옵션을 볼 수 없는 것 같다.


### Reference

> https://wiki.archlinux.org/index.php/file_systems#Mount_a_file_system

> https://wiki.archlinux.org/index.php/Fstab#Tips_and_tricks

> https://unix.stackexchange.com/questions/413823/editing-etc-fstab-to-permanently-bind-mount-directory