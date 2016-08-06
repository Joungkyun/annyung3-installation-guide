# 안녕 리눅스 3 Troubleshooting

이 문서는 안녕 리눅스 3을 설치 함에 있어 특이 사항을 기록해 놓는다.

## 1. HP G5 시리즈

HP G5 시리즈 (DL360 G5, DL380 G5 등)는 RHEL 7 커널 부터 지원을 하지 않습니다. 이를 해결 하기 위해서는 부팅시에 kernel parameter에 다음의 옵션을 추가 해 줘야 합니다. 물론 설치 후에 처음 부팅시에도 넣어 주어야 하며, 처음 부팅 후에, grub2 kernel paramter에도 수동으로 추가를 해 줘야 합니다.

```ini
hpsa.hpsa_allow_any=1
```

