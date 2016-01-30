# CentOS 7 또는 RHEL 7 Network Install ISO를 이용한 설치

**Copyright 2016 &copy; JoungKyun.Kim all rights reserved.**

2016.01.30<br>
김정균 &lt; http://oops.org &gt;

Not Yet!

이 문서는 CentOS 7 또는 RHEL 7의 Netinstall ISO를 이용하셔 설치 하는 방법에 대하여 기술합니다.

이 문서는 Windows용 VirtualBox에서 CentOS 7의 Netinsatll ISO image를 이용하여 설치를 하는 이미지를 보여줍니다. 이 이미지는 PC나 서버에 CDROM 또는 USB 설치시에 동일하게 적용이 됩니다.

또한, Netinstall ISO를 이용하여 부팅 매체(CD 또는 USB)를 만드는 방법은 여기서 다루지 않으니, 인터넷에서 검색을 하여 준비를 하여야 합니다. Netinstall ISO의 버전은 7.x 대이면 어떤 버전이든 상관이 없습니다. 안녕 리눅스 전환시에 최신 버전으로 업데이트가 됩니다.

다음의 설명은 일반적인 CentOS 7이나 RHEL 7의 설치와 동일하며, 안녕 설치를 좀 더 깔끔하게 할 수 있는 옵션 선정을 제공 합니다.

## 1. CDROM 또는 USB 부팅

준비한 Netinstall ISO를 이용하여 만든 booting 매채(CDROM or USB)를 이용하여 booting 을 합니다.

![](VirtualBox_AnNyung3_22_01_2016_19_02_05.png)

Installer 가 구동이 되면 제일 처음은 위와 같은 화면이 나오게 됩니다.

화살표 키를 이용하여 이미지 상의 붉은 색 상자로 표시되어 있는 "**Install CentOS 7**" 을 선택을 선택한 후에, "**Tab**" 키를 누릅니다. 그러면 아래의 이미지와 같이 하단에 booting option을 입력할 수 있게 됩니다. 만약 UEFI 기반의 시스템일 경우에는 "**e**"키를 눌러서 booting option을 입력할 수 있습니다.

이 부분이 잘 이해가 되지 않는다면 [RHEL 7 설치 가이드](https://access.redhat.com/documentation/ko-KR/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/)의 [부트메뉴](https://access.redhat.com/documentation/ko-KR/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/sect-boot-menu-x86.html) 섹션을 참고 하십시오.

![](VirtualBox_AnNyung3_30_01_2016_17_23_08.png)

여기에 아래와 같이 안녕 리눅스 설치를 위한 옵션을 추가해 줍니다.

![](VirtualBox_AnNyung3_22_01_2016_19_03_12.png)

RHEL 7에서 systemd를 도입하면서, installer인 Anaconda에도 systemd가 도입이 되면서 네트워크 인스톨 시에 IP를 입력하던 UI가 사라지고 이처럼 command line에서 IP를 지정을 해 줘야 하는 불편함이 생겼습니다. 여기서 IP를 지정하지 않아도 installer상에서 설정이 가능하지만, 그렇데 된다면 kickstart를 network으로 받아오지 못하는 관계로 command line option으로 IP를 지정해 줘야 합니다.

> utf8 noipv6 ip=192.168.0.227::192.168.0.1:255.255.255.0:annyung3.oops.org::none nameserver=8.8.8.8 inst.ks=http://mirror.oops.org/pub/AnNyung/3/inst/AnNyung.ks

command option으로 위와 같이 옵션을 추가해 주도록 합니다. ip는 여러분의 상황에 맞게 수정을 해야 합니다. 각 옵션에 대한 설명은 다음과 같습니다.

* utf8
 * installer의 언어셋과 설치 후의 언어셋
* noipv6
* ip
* nameserver
* inst.ks

 부팅 옵션에 대한 자세한 설명은 [RHEL 7 설치 가이드](https://access.redhat.com/documentation/ko-KR/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/)의 [부트옵션](https://access.redhat.com/documentation/ko-KR/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-anaconda-boot-options.html) 섹션을 참고 하십시오.