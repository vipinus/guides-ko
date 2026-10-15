# 04 · OpenVPN: .ovpn 프로필을 받아 가져오고 연결하기, 공유기·NAS·Linux에서도 사용

> 웹사이트 버전(더 자세함): https://www.leotun.com/ko/guides/openvpn-setup?utm_source=github&utm_content=client-04

OpenVPN은 오래된 오픈소스 프로토콜로, 거의 모든 운영 체제와 공유기 펌웨어, NAS에 클라이언트가 들어 있습니다. LeoTun의 프로필 파일에는 계정, 비밀번호, 암호화 자료가 이미 들어 있어서 가져오기만 하면 바로 연결됩니다. 휴대폰과 컴퓨터에서 일상적으로 쓴다면 AnyConnect나 Hiddify가 더 편하고, OpenVPN의 가치는 **OpenVPN만 받는 곳**에 있습니다. OpenWrt 공유기, Synology / QNAP NAS, Linux 서버, 오래된 기기 같은 곳입니다.

## 세 단계

1. [웹사이트의 OpenVPN 페이지](https://www.leotun.com/ko/openvpn?utm_source=github&utm_content=client-04) 표에서 내 시스템용 클라이언트를 설치합니다(모든 플랫폼에 공식 OpenVPN Connect가 있고, Windows에서는 OpenVPN GUI, macOS에서는 Tunnelblick도 쓸 수 있습니다).
2. 로그인한 뒤 **지역 국기를 누르면** 그 지역의 .ovpn을 받습니다. 지역마다 파일 하나입니다.
3. 클라이언트에서 파일을 열고 연결합니다.

| 플랫폼 | 설명 |
|---|---|
| Windows / macOS / Android / iOS | 프로필에 계정과 비밀번호가 들어 있으니 가져와서 연결하면 됩니다 |
| Linux | 시스템 VPN 설정 → 파일에서 가져오기, 처음 연결할 때 웹사이트 이메일과 비밀번호 입력. 명령줄은 `openvpn --config file`, 부팅 시 자동 시작하려면 `/etc/openvpn/client/`에 넣으세요 |
| OpenWrt 공유기 | luci-app-openvpn을 설치하고 .ovpn을 올려 활성화합니다. 이 사이트의 펌웨어가 설치되어 있다면 필요 없습니다 |
| Synology NAS | 제어판 → 네트워크 → 네트워크 인터페이스 → 생성 → VPN → OpenVPN(.ovpn 가져오기). NAS의 나가는 트래픽을 회선으로 보내려면 '원격 네트워크에서 기본 게이트웨이 사용'을 체크하세요 |
| QNAP NAS | QVPN → VPN Client → 추가 → OpenVPN, 가져오기 |

## 중국에 있는 사용자: 중국 웹사이트는 직접 연결

연결하면 중국 웹사이트로 가는 트래픽이 돌아가게 됩니다. 웹사이트에서 제공하는 '국내 직결 도구'(중국 IP 직접 연결 도구)를 더블클릭해 실행하면 중국 IP는 직접, 나머지는 회선으로 갑니다. Cisco와 OpenVPN 모두에서 작동합니다. 중국 밖에 있는 사용자는 쓰지 마세요.

## 연결되지 않으면 이 순서로 확인하세요

| 로그 키워드 / 증상 | 원인 | 대처 |
|---|---|---|
| AUTH_FAILED | 계정이나 비밀번호가 틀렸거나 만료됨 | 웹사이트에 로그인해 만료일을 확인하세요. 비밀번호를 바꿨다면 프로필을 다시 받으세요 |
| UDP가 먼저 시간 초과된 뒤 TCP로 연결됨 | 현재 네트워크가 UDP를 제한해 자동으로 TCP로 전환됨 | 쓸 수는 있지만 느립니다. 너무 느리면 네트워크를 바꾸거나 AnyConnect를 쓰세요 |
| UDP와 TCP 모두 TLS handshake failed / key negotiation failed | 서버까지 가는 네트워크 경로가 막힘 | 지역이나 네트워크를 바꾸세요 |
| 가져올 때 오류 | 클라이언트가 너무 오래됨(OpenVPN 2.5 이전) | 클라이언트를 업데이트하세요 |
| 연결 중 갑자기 끊김 | 계정이 만료되어 서버가 연결을 끊음 | 연장한 뒤 다시 연결하세요. 프로필은 바꿀 필요 없습니다 |

## UDP냐 TCP냐

둘 다 들어 있으니 고를 필요가 없습니다. 프로필에서 UDP가 먼저 나오므로 클라이언트는 UDP를 먼저 시도하고, UDP가 제한되거나 연결되지 않으면 몇 초 뒤 자동으로 TCP로 바꿉니다. UDP가 지연이 낮고 빠르며, TCP는 예비용일 뿐이라 국경을 넘을 때 눈에 띄게 느립니다. UDP를 늘 제한하는 네트워크(일부 학교·회사 네트워크)에서는 처음부터 AnyConnect를 쓰는 것을 권합니다.

> 2026년 9월 15일 이전에 받은 프로필에는 UDP만 들어 있습니다. 자동 전환을 원하면 다시 받으세요.

## 보안

프로필 파일에는 계정과 비밀번호가 들어 있어 계정 그 자체와 같으니 남에게 넘기지 마세요. 유출되었다면 웹사이트에서 비밀번호를 바꾸면 예전 파일은 즉시 쓸 수 없게 됩니다. 핸드셰이크 자체도 암호화되어 있어서, 프로필 안의 키가 없으면 핸드셰이크를 시작조차 할 수 없고 스캐너에는 서버가 보이지 않습니다.

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=client-04) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=client-04)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 24시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 개인 요금제 20일을 받으며 상시 진행하는 혜택입니다
