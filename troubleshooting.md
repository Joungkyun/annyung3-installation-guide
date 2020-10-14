# Troubleshooting

이 문서는 안녕 리눅스 3을 설치 함에 있어 특이 사항을 기록해 놓습니다.

## 1. HP Smart Array P400i 설치 문제

RHEL/CentOS 7 부터는 HP DL G1~G5 시리즈에 대해서 더 이상 보증을 하지 않습니다. 안녕 리눅스 3 역시 RHEL 7 기반이기 때문에 동일하게 HP DL G1~G5 까지는 certify를 하지 않습니다.

이 certify의 맥락은 HP Smart Array driver에 대한 문제 입니다. G1 ~ G5 까지는 _**cciss**_ 커널 모듈을 사용하는데, RHEL 7 부터 이 _**cciss**_ 모듈을 제거해 버린 것이 이유 입니다.

_**cciss**_ 모듈을 사용하는 Smart Array 목록은 다음과 같습니다.

* Smart Array 5300 
* Smart Array 5i 
* Smart Array 532 
* Smart Array 5312 
* Smart Array 641 
* Smart Array 642 
* Smart Array 6400 
* Smart Array 6400 EM 
* Smart Array 6i 
* Smart Array P600 
* Smart Array P800 
* Smart Array P400 
* Smart Array P400i 
* Smart Array E200i 
* Smart Array E200 
* Smart Array E500 
* Smart Array P700M

하지만, 꼭 사용 해야겠다면 다음의 방법을 이용할 수 있습니다. \(물론 보증은 하지 않으며, 이 방법을 사용함에 있어 발생한 문제는 누구도 보증하지 않습니다.\)

Install 시에 부팅 편집 모드로 들어가서 kernel parameter에 다음의 옵션을 추가 합니다.

```bash
hpsa.hpsa_allow_any=1
```

설치를 마친 후, 처음 부팅 시에도 부팅 메뉴에서 부팅 편집 모드로 들어가서 위의 옵션을 kernel parameter에 추가해 줍니다.

처음 부팅이 성공 했다면, 부팅시 마다 이 귀찮음을 피하기 위하여 _**GRUB**_에 설정값을 반영해 줍니다.

먼저 _**/etc/default/grub**_ 파일에 위의 옵션을 추가해 줍니다. 혹시 모르니 기존의 설정 파일은 백업을 합니다.

```bash
[root@an3 ~]$ cp -af /etc/default/grub /etc/default/grub.orig
[root@an3 ~]$ perl -pi -e 's/(GRUB_CMDLINE_LINUX="[^"]+)"/\1 hpsa.hpsa_allow_any=1"/g' /etc/default/grub
[root@an3 ~]$
```

다음 _**/etc/default/grub**_에 잘 등록이 되었는지 확인해 봅니다.

```bash
[root@an3 ~]$ cat /etc/default/grub
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="rhgb quiet vga=773 net.ifnames=0 hpsa.hpsa_allow_any=1"
GRUB_DISABLE_RECOVERY="true"
[root@an3 ~]$
```

_**GRUB\_CMDLINE\_LINUX**_ 변수 값에 _**hpsa.hpsa\_allow\_any=1**_ 이 추가 되었는지 확인을 합니다. 제대로 등록이 되었다면 이제 grub에 이 설정을 반영 합니다.

```bash
[root@an3 ~]$ grub2-mkconfig -o /boot/grub2/grub.cfg
[root@an3 ~]$
```

잘 등록이 되었는지 확인해 봅니다.

```bash
[root@an3 ~]$ grep "hpsa.hpsa_allow_any" /boot/grub2/grub.cfg >& /dev/null; [ $? -eq 0 ] && echo "registed" || echo "Not registed"
registed
[root@an3 ~]$
```

다음, 리부팅을 하여 확인을 해 봅니다.

_**참조:**_ 1. [http://serverfault.com/questions/611182/centos-7-x64-and-hp-proliant-dl360-g5-scsi-controller-compatibility](http://serverfault.com/questions/611182/centos-7-x64-and-hp-proliant-dl360-g5-scsi-controller-compatibility) 2. [https://www.centos.org/forums/viewtopic.php?f=49&t=48032](https://www.centos.org/forums/viewtopic.php?f=49&t=48032) 3. [https://wiki.sabayon.org/index.php?title=HOWTO:\_Using\_Custom\_Framebuffer\_Resolution\_with\_GRUB2](https://wiki.sabayon.org/index.php?title=HOWTO:_Using_Custom_Framebuffer_Resolution_with_GRUB2) 4. [https://kldp.org/node/154906](https://kldp.org/node/154906)

