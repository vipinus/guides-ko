# 01 · Cisco AnyConnect: 모든 플랫폼에서 설치, 연결, 업데이트하기

> 웹사이트 버전(더 자세함): https://www.leotun.com/ko/guides/anyconnect-china?utm_source=github&utm_content=client-01

AnyConnect는 Cisco의 기업용 VPN 클라이언트입니다. 지금 공식 이름은 **Cisco Secure Client**이며 사용법은 같습니다. 인증서 파일이나 프로필을 가져올 필요 없이 주소, 계정, 비밀번호만 입력하면 연결됩니다. 중국에서 작동하는지, 연결되지 않을 때 무엇으로 바꿀지는 [중국에서 해외 서비스 접속하기 02](https://github.com/vipinus/guides-zh-CN/blob/main/overseas-access/02-anyconnect-in-china.md)(중국어)를 보세요.

## 설치

| 플랫폼 | 설치할 것 | 받는 곳 |
|---|---|---|
| Windows 10 이상 | Cisco Secure Client 5.x | [웹사이트의 Cisco 페이지](https://www.leotun.com/ko/anyconnect?utm_source=github&utm_content=client-01) |
| Windows 7 / 8 | AnyConnect 4.9(이 버전들을 지원하는 마지막 버전, 더 이상 업데이트 없음) | 위와 같음 |
| macOS | Cisco Secure Client 5.x | 위와 같음 |
| iOS | Cisco Secure Client | App Store. 스토어에 없으면 같은 프로토콜을 쓰는 오픈소스 OpenConnect를 설치하세요 |
| Android | Cisco Secure Client | Google Play 또는 웹사이트 페이지의 APK |
| Linux | 웹사이트 페이지의 설치 파일, 또는 배포판 저장소의 openconnect | 위와 같음 |

Windows에는 오픈소스 OpenConnect-GUI도 있으며, 같은 계정으로 쓸 수 있습니다.

## 네 단계로 연결하기

1. 클라이언트를 열고 주소 칸에 서버 주소를 입력합니다. LeoTun 사용자는 웹사이트에서 **지역 국기를 누르면** 그 지역의 주소가 복사됩니다.
2. 계정(가입한 이메일)과 비밀번호를 입력합니다.
3. 'Connected'(연결됨)가 보이면 IP를 보여 주는 웹페이지를 열어 출구가 고른 지역인지 확인합니다.
4. 지역을 바꾸려면 다른 주소를 쓰면 됩니다. 클라이언트가 써 본 주소를 기억하므로 다음에는 드롭다운 목록에서 고를 수 있습니다.

## 업데이트

먼저 제거할 필요 없이 새 버전을 기존 버전 위에 설치하면 저장된 주소가 그대로 남습니다. 휴대폰은 앱 스토어에서 업데이트하세요. 운영 체제를 크게 업그레이드한 뒤에는 먼저 클라이언트를 업데이트하고 나서 연결 문제를 살펴보세요.

## 자주 보는 메시지

| 메시지 | 뜻 |
|---|---|
| Login failed | 계정이나 비밀번호가 틀렸거나 계정이 만료됨 |
| Untrusted server certificate | 시스템 시계가 틀렸거나, 현재 네트워크가 암호화된 연결을 가로채고 있을 가능성이 큼. 다른 네트워크로 시도하세요 |
| Connection attempt has failed | 이 주소에 잠시 연결할 수 없음. 지역을 바꾸세요 |

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=client-01) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=client-01)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 4시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 15크레딧(개인 요금제로 약 15일)을 받으며 상시 진행하는 혜택입니다
