

# Virtual box on centos

- Vboxdrv 커널 빌드를 하기위한 모듈 다운로드
```
$sudo yum install -y kernel-devel kernel-headers make patch gcc 
```
- Oracle lunar repo 파일 다운로드
```
$sudo wget https://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -P /etc/yum.repos.d 
```

- Virtual box 5.2 다운로드(y 입력)
```
$sudo yum install -y VirtualBox-5.2
```

- Virtual box 설치 확인
```
$systemctl status vboxdrv
```

> 상태가 아직 살아있지 않다면 아래와 같이 표시됩니다

```
[root@k8s-master ldccai]# systemctl status vboxdrv
● vboxdrv.service - VirtualBox Linux kernel module
   Loaded: loaded (/usr/lib/virtualbox/vboxdrv.sh; enabled; vendor preset: disabled)
   Active: inactive (dead)
```

살립시다..
```
$systemctl start vboxdrv
```

> 시작이 안되네요… 
```
[root@k8s-master ldccai]# systemctl start vboxdrv
Job for vboxdrv.service failed because the control process exited with error code. See "systemctl status vboxdrv.service" and "journalctl -xe" for details
```

- Journalctl -xe 명령어를 통해 로그를 확인해봅시다…;

```
pr 28 09:24:35 k8s-master systemd[1]: vboxdrv.service: control process exited, code=exited status=1
Apr 28 09:24:35 k8s-master systemd[1]: Failed to start VirtualBox Linux kernel module.
-- Subject: Unit vboxdrv.service has failed
-- Defined-By: systemd
-- Support: http://lists.freedesktop.org/mailman/listinfo/systemd-devel
--
-- Unit vboxdrv.service has failed.
--
-- The result is failed.
Apr 28 09:24:35 k8s-master systemd[1]: Unit vboxdrv.service entered failed state.
Apr 28 09:24:35 k8s-master systemd[1]: vboxdrv.service failed.
Apr 28 09:24:35 k8s-master polkitd[579]: Unregistered Authentication Agent for unix-process:27030:203110 (sy
```

>이슈를 검색해 봅시다 …
```
Unregistered Authentication Agent for unix-process
```

> 잘안나오네요.. 로그를 다시확인해봅시다…

```
[root@k8s-master ldccai]# systemctl status vboxdrv.service
● vboxdrv.service - VirtualBox Linux kernel module
   Loaded: loaded (/usr/lib/virtualbox/vboxdrv.sh; enabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Tue 2020-04-28 09:34:56 UTC; 19s ago
  Process: 27530 ExecStart=/usr/lib/virtualbox/vboxdrv.sh start (code=exited, status=1/FAILURE)

Apr 28 09:34:56 k8s-master vboxdrv.sh[27530]: vboxdrv.sh: Building VirtualBox kernel modules.
Apr 28 09:34:56 k8s-master vboxdrv.sh[27530]: This system is currently not set up to build kernel modules.
Apr 28 09:34:56 k8s-master vboxdrv.sh[27530]: Please install the Linux kernel "header" files matching...rnel
Apr 28 09:34:56 k8s-master vboxdrv.sh[27530]: for adding new hardware support to the system.
Apr 28 09:34:56 k8s-master vboxdrv.sh[27530]: The distribution packages containing the headers are probably:
Apr 28 09:34:56 k8s-master vboxdrv.sh[27530]: kernel-devel kernel-devel-3.10.0-862.11.6.el7.x86_64
Apr 28 09:34:56 k8s-master systemd[1]: vboxdrv.service: control process exited, code=exited status=1
Apr 28 09:34:56 k8s-master systemd[1]: Failed to start VirtualBox Linux kernel module.
Apr 28 09:34:56 k8s-master systemd[1]: Unit vboxdrv.service entered failed state.
Apr 28 09:34:56 k8s-master systemd[1]: vboxdrv.service failed.
Hint: Some lines were ellipsized, use -l to show in full.
```

> 아… gui 가 없어서 그렇구나… ;;


ref : https://linuxize.com/post/how-to-install-virtualbox-on-centos-7/



