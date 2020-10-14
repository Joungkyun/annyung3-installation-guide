# AnNyung 3 Upgrade

이 문서는 안녕 리눅스 2에서 안녕 리눅스 3으로의 upgrade에 대해서 권고 합니다.

결론적으로, 안녕 2에서 안녕 3으로의 upgrade는 _**공식적으로 권장하지 않습니다.**_

CentOS 7은 공식적으로 "[https://wiki.centos.org/TipsAndTricks/CentOSUpgradeTool](https://wiki.centos.org/TipsAndTricks/CentOSUpgradeTool)" 문서에서 centos-upgrade-tool 이라는 CentOS 7 upgrade 도구를 제공 하고 있습니다.

하지만 CentOS 6\_5 부터 일부 CentOS 6의 패키지들의 버전이 CentOS 7보다 높아서 업그레이드시에 완전하지 못한 문제가 발생함으로서 사용 권장을 하지 않는 이슈들이 꽤 있습니다.

필자 역시 테스트 중, CentOS 6의 grub 를 CentOS 7의 grub2 로 migration 하는 중에 많은 문제를 마주쳤으며, CentOS 7의 kernel upgrade 시에 중요한 device module들이 누락되어 업그레이드 되어 설치 완료 후 부팅이 되지 않는 문제가 복불복으로 발생을 하였습니다.

현재 centos-upgrade-tool을 안녕에서 사용할 수 있도록 하는 작업은 완료된 상태이나, CentOS의 centos-upgrade-tool을 이용한 upgrade가 완전하지 못한 까닭으로, 안녕 리눅스 3에서는 공식적으로 안녕 2에서 안녕 3으로의 upgrade는 권장하지 않으며, _**새로 설치할 것을 아주 강력하게 권고 합니다.**_

