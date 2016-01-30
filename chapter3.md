# Xen Server의 guest os로 설치

Not Yet!
**Copyright 2016 &copy; JoungKyun.Kim all rights reserved.**

2016.01.30<br>
김정균 &lt; http://oops.org &gt;

이 문서는 Xen Server에 안녕 리눅스 3을 설치하는 방법을 기술 합니다.

이 문서는 Windows용 Citrix XenCenter를 이용하여 설치하는 방법을 보여주며, Installer가 실행된 다음 부터는 <a href="chapter2.html">"**2. CentOS/RHEL 7 Network Insatll ISO를 이용한 설치**"</a> 와 동일하게 진행이 됩니다.

이 문서에서는 Xen Center를 이용하여 OS를 설치하는 과정을 모두 설명하지는 않습니다.


## 1. New VM 생성

geust OS를 생성하기 위하여 Xen Center를 실행하고, 상단 툴바에서 "**_New VM_**" 을 선택 합니다.


## 2. Select a VM template

![템플릿 선택 이미지](xen-001.jpg)

여기서는 Xen server가 remote에 있다는 가정하에 진행을 합니다.

CentOS 7 template을 선택할 경우, Xen server의 local cdrom 또는 Bootp만 부팅에 사용을 할 수 있기 때문에 많은 귀찮음이 있습니다. 그래서 여기서는 CentOS 6 template을 사용하여 설치를 진행합니다.

그러므로, template은 **_CentOS 6 (64-bit)_** 을 선택하도록 합니다.


## 3. Name 설정

![Name 설정 이미지](xen-002.jpg)

Xen Center의 트리에 보여지는 이름을 설정 합니다. 보통은 서버의 hostname을 지정해 주시면 됩니다. 역시 여기의 설정은 OS 설치에는 영향을 주지 않으며, 단순히 Xen Center에서 현재 만드는 VM을 인식하기 위한 정보로만 사용이 됩니다.


## 4. Insatll Media 설정

![Insatll Media 설정 이미지](xen-003.jpg)

installation method는 "**Insatll From URL:**"을 선택 하도록 하고 CentOS 7의 boot image가 있는 URL을 지정해 줍니다. 한국의 mirror는 다음 중에 하나를 사용하실 수 있습니다.

> 1. http://ftp.daum.net/centos/7/os/x86_64
2. http://centos.tt.co.kr/7/os/x86_64
3. http://centos.mirror.cdnetworks.com/7/os/x86_64

다음, 하단의 "**Advanced OS boot parameters**"에 다음의 옵션을 추가해 줍니다.

    ip=YOUR_SERVER_IP::GATEWAY_IP:SUBNET_MASK:HOSTNAME::none nameserver=8.8.8.8 inst.ks=http://mirror.oops.org/pub/AnNyung/3/inst/AnNyung.ks inst.vnc

안녕 리눅스 2에서 처럼 asknetwork은 더이상 지원하지 않기 때문에, boot parameters에서 이제는 IP설정을 직접 해 줘야 합니다.

