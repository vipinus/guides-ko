# 06 · iOS에서 앱을 설치할 수 없을 때

iPhone에서 Hiddify, Tailscale, Telegram을 찾을 수 없거나 '이 앱은 현재 사용자의 국가 또는 지역에서 사용할 수 없습니다'라는 메시지가 뜬다면, 앱이 사라진 것이 아닙니다. App Store는 Apple ID의 지역별로 스토어가 나뉘어 있고, 중국 스토어에는 네트워크 관련 앱이 대부분 올라와 있지 않습니다. iOS에서는 중국 외 지역 Apple ID로 App Store에서 설치하면 되며, 방법은 이 페이지에 있습니다. 기존 계정의 지역을 바꾸기보다 새 계정을 만드는 것을 권합니다. 아래에 단계, 결제 수단을 '없음'으로 고르는 요령, 그리고 남이 공유한 계정을 절대 쓰면 안 되는 이유를 정리했습니다.

## 왜 이런 일이 생기나요

App Store는 Apple ID의 지역별로 스토어가 나뉘고, 지역마다 올라와 있는 앱이 다릅니다. 중국 스토어에는 Hiddify도 Tailscale도 없고, Telegram과 Discord는 있다 없다 합니다. Cisco Secure Client와 OpenVPN Connect는 대부분의 지역에 있습니다. 앱의 문제가 아니라 진열의 차이이며, 다른 지역 계정이면 설치할 수 있습니다.

iPhone에서는 이 사이트의 Hiddify와 사설망(Tailscale) 모두 App Store에서 설치합니다. 아래 단계대로 다른 지역 Apple ID로 바꾸기만 하면 됩니다. Android, Windows, macOS용 설치 파일은 이 사이트에서 직접 제공하므로 영향이 없습니다.

## 방법 1(권장): 중국 외 지역 Apple ID 새로 만들기

1. 현재 App Store 계정에서 로그아웃합니다: 설정 → 맨 위의 내 이름 → 미디어 및 구입 항목 → 로그아웃. App Store에서만 로그아웃되고 iCloud는 그대로라서 사진, 백업, 연락처에는 영향이 없습니다.
2. App Store에서 무료 앱을 하나 찾아 '받기'를 누르고, 안내에 따라 '새로운 Apple 계정 만들기'를 진행합니다. 지역은 미국, 홍콩, 일본, 싱가포르 중 아무거나 고르고, 결제 수단은 '없음'을 고르세요. 이 '없음'은 무료 앱을 받으면서 가입하는 경로에서만 나타나며, 웹에서 바로 가입하면 대개 나오지 않습니다.
3. 새 계정으로 App Store에 로그인한 뒤 Hiddify, Tailscale, Telegram을 검색해 내려받습니다.
4. 설치가 끝나면 원래 계정으로 돌아가도 됩니다. 이미 설치된 앱은 평소대로 작동하고 업데이트도 됩니다. 새 앱을 설치해야 할 때 다시 바꾸면 됩니다.

## 방법 2: 기존 계정의 지역 바꾸기

account.apple.com에 로그인해 국가 또는 지역을 바꿉니다. 먼저 모든 구독을 해지하고 잔액을 다 써야 하며, 경우에 따라 현지 결제 수단도 추가해야 하고, 되돌리는 것도 똑같이 번거롭습니다. 어차피 장기적으로 지역을 바꿀 생각이 아니라면 권하지 않습니다.

## 절대 하면 안 되는 일

- 남이 공유한 Apple ID를 쓰지 마세요. 그룹이나 인터넷의 '공유 계정'도 마찬가지입니다. 계정 주인이 원격으로 기기를 잠글 수 있고, 잠긴 iPhone은 그 사람만 풀 수 있습니다. 이중 인증이 켜지면 끌 수 없으며, 위험과 분쟁은 모두 내가 떠안게 됩니다. 이 사이트의 고객 지원도 공유 계정은 일절 제공하지 않습니다.
- 출처를 알 수 없는 구성 프로파일이나 '엔터프라이즈 인증서로 서명된' 설치 파일을 설치하지 마세요. 스토어를 우회하는 흔한 수법이자, 인증서를 심어 트래픽을 가로채는 통로이기도 합니다.

## 설치한 뒤

Hiddify: 이 사이트의 Hiddify 페이지로 돌아가 코드를 스캔하거나, 'sing-box 구독' 버튼을 눌러 복사한 뒤 Hiddify로 전환해 추가합니다. Tailscale: 먼저 공식 계정에서 로그아웃한 뒤, 사설망 페이지의 단계대로 이 사이트의 컨트롤 서버 주소를 입력합니다. Telegram, Discord: 이 사이트의 문의 페이지에서 코드를 스캔해 그룹에 들어오세요.

## 자주 묻는 질문

**다른 지역에 가입하려면 신용카드가 필요한가요?** 아닙니다. 방법 1의 경로(무료 앱을 받으면서 가입)에서는 결제 수단으로 '없음'을 고를 수 있습니다.

**새 계정이 iCloud와 사진에 영향을 주나요?** 아닙니다. 계정은 App Store에서만 바꾸고, iCloud는 원래 계정 그대로입니다.

**iPad도 같은가요?** 네, iPadOS도 같은 App Store 규칙을 따릅니다.

**Android 휴대폰도 이런 문제가 있나요?** 없습니다. Android, Windows, macOS, Linux용 설치 파일은 이 사이트에서 직접 배포하며 앱 스토어에 의존하지 않습니다.

## 더 읽을거리

- [문의 페이지: 클라이언트 다운로드 카드와 세 그룹](https://www.leotun.com/ko/contact?utm_source=github&utm_content=client-06)
- [Hiddify: 코드를 스캔해 가져오기](https://www.leotun.com/ko/singbox?utm_source=github&utm_content=client-06)
- [사설망(Tailscale): 로그인 단계](https://www.leotun.com/ko/mesh?utm_source=github&utm_content=client-06)
- [연락하는 법과 연락이 끊기지 않게 하는 법](https://www.leotun.com/ko/guides/stay-in-touch?utm_source=github&utm_content=client-06)

이 글의 웹사이트 버전: https://www.leotun.com/ko/guides/ios-app-store?utm_source=github&utm_content=client-06

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=client-06) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=client-06)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 4시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 15크레딧(개인 요금제로 약 15일)을 받으며 상시 진행하는 혜택입니다
