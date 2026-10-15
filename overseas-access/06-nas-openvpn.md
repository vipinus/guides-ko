# 06 · Synology나 QNAP NAS를 회선으로 보내는 법

NAS는 집에서 회선이 가장 필요하면서도 가장 신경을 덜 쓰는 기기입니다. 다운로더는 해외 자료에 닿아야 하고, Docker는 이미지를 받아야 하고, Cloud Sync는 해외 클라우드 드라이브와 동기화해야 하고, Plex는 메타데이터를 가져와야 합니다. NAS에서는 Hiddify를 돌릴 수 없지만, Synology와 QNAP 모두 OpenVPN 클라이언트를 기본으로 갖고 있습니다. 이 사이트의 OpenVPN 페이지에서 .ovpn을 받아 가져오면 연결되고, 부팅할 때 자동으로 다시 연결됩니다. 이 글은 Synology와 QNAP에서 가져오기 메뉴가 어디 있는지, 핵심 옵션인 '기본 게이트웨이 사용', 비밀번호를 바꾼 뒤 할 일, 그리고 '밖에서 NAS에 접속하기'는 왜 별개의 일이며 사설망이 필요한지를 다룹니다.

## 먼저 두 가지를 구분하세요

NAS 자체를 회선으로 보내기(다운로드, 이미지 받기, 해외 클라우드 드라이브 동기화): OpenVPN을 씁니다. 이 글에서 다루는 내용입니다.

밖에서 NAS에 접속하기(출장 중에 공유 폴더 열기, 카메라 보기): 사설망(Tailscale)을 써서 NAS와 휴대폰을 같은 사설망에 넣습니다. '해외에서 중국 집의 카메라와 NAS 보기'를 보세요. 이 일은 사설망에 맡기세요. OpenVPN은 NAS를 저희 회선에 연결하고, 사설망은 나를 집 안으로 연결합니다.

## Synology

1. 이 사이트에 로그인해 OpenVPN 페이지에서 지역의 국기를 누르면 그 지역의 .ovpn 파일이 내려받아집니다.
2. 제어판 → 네트워크 → 네트워크 인터페이스 → 생성 → VPN 프로필 생성 → OpenVPN(.ovpn 파일 가져오기)으로 가서 이 사이트 계정의 이메일과 비밀번호를 입력합니다.
3. '원격 네트워크에서 기본 게이트웨이 사용': 체크하면 NAS의 나가는 트래픽이 모두 회선을 거칩니다(다운로드, Docker, Cloud Sync 모두 혜택을 봅니다). 체크하지 않으면 터널만 만들고 나가는 트래픽은 그대로 현지에서 나갑니다. 대부분의 경우 체크해야 합니다.
4. 'VPN 연결이 끊어지면 다시 연결'을 체크해 두면 NAS가 재시작하거나 회선이 흔들려도 자동으로 복구됩니다. 연결한 뒤 패키지에서 한 번 받아 보세요.

## QNAP

1. 같은 방법으로 .ovpn을 받습니다.
2. QVPN Service → VPN Client → 추가 → OpenVPN으로 가서 파일을 가져오고 계정과 비밀번호를 입력합니다.
3. 연결 설정에서 'VPN을 NAS의 기본 게이트웨이로 사용'(Use VPN as the default gateway of the NAS)과 자동 재연결을 체크한 뒤 연결합니다.

## 어떤 트래픽이 거치고 어떤 트래픽은 거치지 않나

- 거치는 것: Download Station / Download Station의 BT·HTTP 작업, Docker 이미지 받기, Cloud Sync의 Google Drive / Dropbox / OneDrive 동기화, Plex와 Emby의 메타데이터 가져오기, 패키지 센터 업데이트.
- 거치지 않는 것: 집 LAN 안에서 내가 NAS에 접속하는 트래픽. 원래 LAN 안이라 영향이 없습니다.
- 중국에 있으면서 중국 사이트는 직접 연결하고 싶을 때: NAS에는 분할 라우팅 스크립트가 없어서, OpenVPN이 연결되면 NAS의 나가는 트래픽이 모두 회선을 거칩니다. 중국의 다운로드 소스가 느리면 다운로드 작업에 중국 미러 주소를 쓰거나, 필요할 때만 회선에 연결하세요.

## 알아 둘 점

- 설정 파일에는 계정 정보가 들어 있고, 비밀번호를 바꾸면 NAS의 비밀번호 칸은 더 이상 통하지 않습니다. .ovpn을 다시 받아 바꾸거나, VPN 프로필에서 비밀번호만 고치세요.
- 계정이 만료되면 NAS의 연결이 끊기고, 연장하면 자동으로 다시 연결되며 설정을 바꿀 필요는 없습니다.
- NAS는 기기 1대로 세고, 다른 기기와 동시 접속 한도를 함께 씁니다(개인 2대, 패밀리 4대, 기업 8대).
- 회선은 UDP 위에서 돌아갑니다. 집 브로드밴드에 있는 NAS가 UDP 제한에 걸리는 일은 거의 없습니다.

## 자주 묻는 질문

**'기본 게이트웨이 사용'을 체크해도 LAN에서 NAS에 접속할 수 있나요?** 네. LAN 트래픽은 게이트웨이를 거치지 않으므로 공유 폴더, Plex 재생, 관리 페이지 모두 영향이 없습니다.

**NAS를 회선으로 보낸 뒤 Plex 원격 재생이 느려졌어요.** Plex 원격 재생은 NAS의 나가는 트래픽을 쓰므로, 기본 게이트웨이를 체크하면 회선을 돌아가게 됩니다. 원격 재생에는 사설망으로 NAS에 접속하는 편이 더 직접적입니다. 아니면 다운로드할 때만 OpenVPN을 연결하세요.

**Download Station만 회선으로 보낼 수 있나요?** Synology와 QNAP에는 앱별 분할 라우팅이 없습니다. 세밀하게 나누려면 Docker에서 OpenVPN이 들어간 다운로드 컨테이너(qbittorrent + gluetun 등)를 돌리고 그것만 회선으로 보내세요.

**Linux 시스템 NAS(TrueNAS, Unraid)는요?** Linux 방식대로 하면 됩니다. openvpn 패키지를 설치하고 설정 파일을 /etc/openvpn/client/에 넣으세요. 'Linux 서버와 명령줄 도구를 회선으로 보내는 법'을 보세요.

## 더 읽을거리

- [OpenVPN 페이지: 클라이언트 다운로드와 설정 파일](https://www.leotun.com/ko/openvpn?utm_source=github&utm_content=overseas-access-06)
- [OpenVPN 쓰는 법과 언제 고를까](https://www.leotun.com/ko/guides/openvpn-setup?utm_source=github&utm_content=overseas-access-06)
- [해외에서 중국 집의 카메라와 NAS 보기](https://www.leotun.com/ko/guides/home-camera?utm_source=github&utm_content=overseas-access-06)
- [Linux 서버와 명령줄 도구를 회선으로 보내는 법](https://www.leotun.com/ko/guides/linux-server?utm_source=github&utm_content=overseas-access-06)

이 글의 웹사이트 버전: https://www.leotun.com/ko/guides/nas-openvpn?utm_source=github&utm_content=overseas-access-06

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=overseas-access-06) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=overseas-access-06)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 24시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 개인 요금제 20일을 받으며 장기간 유효합니다
