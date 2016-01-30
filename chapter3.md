# Xen Server의 guest os로 설치

Not Yet!
**Copyright 2016 &copy; JoungKyun.Kim all rights reserved.**

2016.01.30<br>
김정균 &lt; http://oops.org &gt;

이 문서는 Xen Server에 안녕 리눅스 3을 설치하는 방법을 기술 합니다.

이 문서는 Windows용 Citrix XenCenter를 이용하여 설치하는 방법을 보여주며, Installer가 실행된 다음 부터는 <a href="chapter2.html">"**2. CentOS/RHEL 7 Network Insatll ISO를 이용한 설치**"</a> 와 동일하게 진행이 됩니다.

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