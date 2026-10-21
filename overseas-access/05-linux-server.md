# 05 · Linux 서버와 명령줄 도구를 회선으로 보내는 법

Linux에서 회선을 쓰는 방법은 두 가지이며, 필요에 따라 고르면 됩니다. 머신 전체를 회선으로 보내려면(Docker 이미지 받기, 해외 네트워크가 필요한 서비스 운영, 무인 운영) OpenVPN을 쓰세요. 설정 파일 하나를 /etc/openvpn/client/에 두고 부팅 시 자동 시작하면 됩니다. 명령 몇 개만 회선으로 보내려면(git, pip, npm, curl) 웹 프록시를 쓰세요. 프록시 주소를 http_proxy 환경 변수에 넣으면 나머지 트래픽은 건드리지 않습니다. 데스크톱 Linux에서는 NetworkManager로 가져올 수도 있습니다. 이 글은 세 가지 방법을 모두 다루며, 비밀번호 파일 작성법과 확인 명령도 함께 안내합니다.

## 방법 1: 머신 전체를 회선으로(OpenVPN)

1. 클라이언트 설치: Debian / Ubuntu는 sudo apt install openvpn, Fedora는 sudo dnf install openvpn, Arch는 sudo pacman -S openvpn.
2. 이 사이트에 로그인해 OpenVPN 페이지에서 지역 국기를 눌러 .ovpn을 내려받습니다. Linux용으로 받는 설정에는 계정과 비밀번호가 들어 있지 않으므로(NetworkManager가 계정 정보가 내장된 파일을 받아들이지 않기 때문입니다) 비밀번호 파일을 따로 만듭니다. 두 줄로, 첫 줄은 이 사이트의 이메일, 둘째 줄은 비밀번호이며, chmod 600으로 권한을 설정합니다.
3. .ovpn을 /etc/openvpn/client/<region>.conf로 복사하고, 파일 안의 auth-user-pass 뒤에 비밀번호 파일 경로를 적습니다.
4. sudo systemctl enable --now openvpn-client@<region>. 상태는 systemctl status openvpn-client@<region>으로 보고, curl -s https://ipinfo.io/country 결과가 고른 지역으로 나오는지 확인합니다.
5. 지역을 바꾸려면 다른 설정을 받아 다른 유닛을 활성화합니다. 한 번에 하나만 실행하세요.

## 방법 2: 명령줄 도구만 회선으로(웹 프록시)

이 사이트의 웹 프록시 페이지에 나오는 프록시 주소를 계정, 비밀번호와 함께 환경 변수에 바로 넣으면 됩니다. export https_proxy=https://username:password@proxy-address export http_proxy=$https_proxy. 비밀번호의 특수 문자는 URL 인코딩해야 합니다. 그러면 이 터미널에서 curl, wget, git, pip, npm이 모두 회선을 거치고, 다른 프로그램은 영향을 받지 않습니다.

Docker 데몬은 셸 환경 변수를 읽지 않습니다. /etc/systemd/system/docker.service.d/proxy.conf의 Environment=에 적고 docker를 재시작하세요. apt는 /etc/apt/apt.conf.d/proxy.conf에 Acquire::https::Proxy를 적습니다.

이 방법은 구조상 끊길 연결 자체가 없고, root 권한도 필요 없으며 라우팅도 바꾸지 않습니다. 회사 서버나 다운로드 속도만 높이고 싶을 때 알맞습니다. 프록시 변수를 따르는 프로그램에만 적용되고 나머지 트래픽은 그대로입니다.

## 방법 3: 데스크톱 Linux의 NetworkManager

1. network-manager-openvpn-gnome을 설치합니다(이 사이트의 OpenVPN 페이지에서 클릭 한 번으로 소프트웨어 센터를 열 수 있습니다).
2. 설정 → 네트워크 → VPN → '+' → '파일에서 가져오기'에서 .ovpn을 고르고, 이 사이트의 이메일과 비밀번호를 입력해 저장합니다.
3. 상단 표시줄이나 트레이에서 VPN을 켜고 끕니다. 부팅 시 자동 연결하려면 유선/무선 연결 설정에서 'VPN에 자동으로 연결'을 체크하세요.

## 확인과 문제 해결

- 출구 확인: curl -s https://ipinfo.io 결과의 국가가 고른 지역이면 됩니다.
- DNS 확인: resolvectl status에서 VPN 인터페이스의 DNS가 회선이 내려 준 것이어야 합니다. 새고 있다면 설정에 dhcp-option DNS를 추가하거나 update-systemd-resolved 스크립트를 쓰세요.
- AUTH_FAILED: 비밀번호 파일이 틀렸거나 계정이 만료된 것입니다. 비밀번호를 바꿨다면 비밀번호 파일도 고치세요.
- TLS 핸드셰이크 시간 초과: 서버로 가는 UDP가 통하지 않는 것입니다. 지역이나 네트워크를 바꾸세요. 클라우드 서버라면 보안 그룹에서 아웃바운드 UDP를 허용해야 합니다.
- 서버가 중국에 있고 중국 내 소스는 직접 연결하고 싶을 때: OpenVPN이 연결되면 나가는 트래픽이 모두 회선을 탑니다. apt / pip / npm 소스를 중국 미러로 바꾸거나, 방법 2를 써서 특정 명령만 회선을 거치게 하세요.

## 알아 둘 점

- Linux 머신 한 대는 기기 1대로 세며, 다른 기기와 동시 접속 한도를 나눠 씁니다(개인 2대, 패밀리 4대, 기업 8대). 방법 2의 웹 프록시도 연결 단위로 세어 포함됩니다.
- 설정 파일과 비밀번호 파일은 계정과 같습니다. git 저장소에 커밋하거나 이미지에 넣지 마세요.
- 비밀번호를 바꾸면 예전 설정은 즉시 쓸 수 없게 됩니다. 의도된 폐기 장치입니다. 비밀번호 파일만 고치면 됩니다.
- 클라우드 서버에서 회선을 쓸 때는 해당 업체의 이용 약관을 따르세요. 회선은 접속 시간과 총 데이터량만 기록합니다.

## 자주 묻는 질문

**Linux용 설정에는 왜 계정과 비밀번호가 들어 있지 않나요?** NetworkManager는 계정 정보가 내장된 설정 파일을 가져오면 받아들이지 않고 가져오기 실패를 띄웁니다. 그래서 Linux용으로 발급하는 파일은 직접 입력하게 되어 있고, systemd 방식에서는 비밀번호 파일에 적으면 됩니다.

**Docker만 회선을 타게 할 수 있나요?** 됩니다. Docker 데몬에만 프록시 변수를 설정하거나(방법 2), OpenVPN이 들어 있는 컨테이너(gluetun)를 띄워 특정 컨테이너만 회선을 거치게 하세요.

**Linux에서 사설망(Tailscale)은 어떤가요?** 공식 스크립트로 한 줄이면 설치되고, tailscale up --login-server=<this site's control server>로 로그인합니다. 밖에서 이 머신에 접속해야 하거나 한 번 설정해 두고 늘 온라인으로 두고 싶을 때 알맞습니다. 다운로드 속도만 높이려면 OpenVPN이나 프록시가 더 간단합니다.

**공유기의 OpenWrt도 마찬가지인가요?** OpenWrt에서는 luci-app-openvpn을 설치하고 .ovpn을 올리면 LAN 전체가 회선을 탑니다. 이 사이트의 펌웨어를 올린 공유기는 이 작업이 필요 없고, 계정으로 로그인하기만 하면 됩니다.

## 더 읽을거리

- [OpenVPN 페이지: 클라이언트 다운로드와 설정 파일](https://www.leotun.com/ko/openvpn?utm_source=github&utm_content=overseas-access-05)
- [OpenVPN 사용법과 언제 고르면 좋은가](https://www.leotun.com/ko/guides/openvpn-setup?utm_source=github&utm_content=overseas-access-05)
- [Synology, QNAP NAS를 회선으로 보내는 법](https://www.leotun.com/ko/guides/nas-openvpn?utm_source=github&utm_content=overseas-access-05)
- [웹 프록시란 무엇이고 언제 쓰나](https://www.leotun.com/ko/guides/web-proxy?utm_source=github&utm_content=overseas-access-05)

이 글의 웹사이트 버전: https://www.leotun.com/ko/guides/linux-server?utm_source=github&utm_content=overseas-access-05

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=overseas-access-05) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=overseas-access-05)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 4시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 15크레딧(개인 요금제로 약 15일)을 받으며 장기간 유효합니다
