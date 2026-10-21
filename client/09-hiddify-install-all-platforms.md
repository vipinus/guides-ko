# 09 · 모든 플랫폼에 Hiddify 설치하기: Windows, macOS, Linux, Android, iOS

이 사이트의 Hiddify 메뉴에서 쓰는 클라이언트는 오픈소스 Hiddify입니다. sing-box 코어가 내장되어 있어 설치만 하면 따로 설정할 것이 없습니다. 다섯 플랫폼 모두 같은 앱을 쓰지만 처음 실행할 때 걸리는 부분이 다릅니다. Windows에서는 백신 프로그램이 막거나 지워 버릴 수 있고, Mac에서는 '손상되었다'는 메시지가 뜨는 데다 네트워크 확장 프로그램도 승인해야 하며, Linux에서는 권한 부여 명령을 실행해야 VPN 모드가 켜지고, iPhone에서는 중국 지역 App Store에서 찾을 수 없습니다. 이 글은 플랫폼별로 어디서 받고 어떻게 설치하며 처음 실행할 때 무엇을 해야 하는지 정리하고, 마지막에 구독을 가져와 연결하는 가장 짧은 단계를 안내합니다.

## 어디서 받나요

| 플랫폼 | 설치 파일 | 받는 곳 |
|---|---|---|
| Windows | 설치 프로그램(.exe), x64 전용 | Hiddify 페이지의 다운로드 영역 |
| macOS | .dmg, Apple 실리콘과 Intel 공용 패키지 하나 | Hiddify 페이지의 다운로드 영역 |
| Linux | .deb(Debian / Ubuntu 계열), x64 전용 | Hiddify 페이지의 다운로드 영역 |
| Android | .apk, ARM64와 x86-64 두 가지 | Hiddify 페이지의 다운로드 영역 또는 Google Play |
| iPhone / iPad | App Store의 Hiddify Proxy & VPN | App Store, 중국 외 지역 Apple ID 필요 |

Hiddify 페이지의 다운로드 영역은 지금 쓰는 시스템에 맞는 패키지를 자동으로 추천하고, 다른 시스템용 패키지는 그 아래에 나열합니다. 각 줄 옆에는 Hiddify 공식 릴리스 페이지로 가는 '공식 사이트' 아이콘도 있어 버전을 비교해 볼 수 있습니다. 데스크톱 세 시스템(Windows, macOS, Linux)은 동영상 튜토리얼도 있습니다.

데스크톱 설치 파일은 Hiddify 공식 릴리스 패키지를 그대로 옮겨 둔 미러이며, 수정하거나 다시 패키징하지 않았습니다. 허용하기 전에 직접 확인해 볼 수도 있습니다. 설치 파일을 VirusTotal에 올려 보면 됩니다. 방법은 [문제 해결 06](../troubleshooting/06-antivirus-false-positive.md)을 보세요.

## Windows

1. Hiddify 페이지의 다운로드 영역에서 설치 프로그램을 받아 더블클릭해 설치합니다. (현재 저희 테스트에서는 Windows 보안이 이 파일을 차단하지 않습니다. 따로 설치한 백신 프로그램이 차단한다면 [문제 해결 06](../troubleshooting/06-antivirus-false-positive.md) 끝의 자주 묻는 질문을 보세요.)

## macOS

1. Hiddify 페이지의 다운로드 영역에서 .dmg를 받아 열고, Hiddify를 '응용 프로그램'으로 끌어다 놓습니다.
2. 'Finder' → '응용 프로그램'에서 Control 키를 누른 채 Hiddify 아이콘을 클릭하고 '열기'를 고른 뒤, 대화상자에서 다시 '열기'를 누릅니다.
3. 그래도 열리지 않으면: '시스템 설정' → '개인정보 보호 및 보안'의 '보안' 항목에서 '그래도 열기'를 누르고 암호를 입력해 확인합니다.
4. '손상되었기 때문에 열 수 없습니다'라는 메시지가 뜨면: 파일이 실제로 손상된 것이 아니라 시스템의 Gatekeeper가 막고 있는 것입니다. '터미널'을 열어 아래 명령을 실행하고 Return 키를 누른 뒤 로그인 암호를 입력하고, Hiddify를 다시 엽니다.

```bash
sudo xattr -dr com.apple.quarantine /Applications/Hiddify.app
```

이 명령은 '인터넷에서 받은 파일'이라는 격리 표시만 지우며, 이 앱 하나에만 적용됩니다. `sudo spctl --master-disable`로 컴퓨터 전체의 Gatekeeper를 끄는 방법은 **쓰지 마세요**.

설치 후 처음 연결을 누르면 시스템이 '네트워크 확장 프로그램' 승인도 요구합니다. 이 단계를 건너뛰면 아이콘이 계속 돌기만 하고 연결되지 않습니다.

- **macOS 15 Sequoia 이상**: '시스템 설정' → '일반' → '로그인 항목 및 확장 프로그램'에서 맨 아래 '확장 프로그램'까지 스크롤하고, 보기 방식을 '카테고리별'로 바꾼 뒤 '네트워크 확장 프로그램' 옆의 ⓘ를 클릭합니다. Hiddify 스위치를 켜고, 안내가 나오면 암호를 입력하거나 Touch ID로 확인합니다.
- **macOS 13 Ventura / 14 Sonoma**: 먼저 Hiddify를 실행해 연결을 한 번 누르면 '시스템 확장 프로그램이 차단됨' 알림이 뜹니다. 그다음 '시스템 설정' → '개인정보 보호 및 보안'에서 아래로 스크롤해 '개발자 …의 시스템 소프트웨어가 로드하지 못하도록 차단됨'을 찾아 '허용'을 누르고 암호를 입력합니다.

회사에서 지급한 Mac에서 이 버튼들이 회색으로 비활성화되어 있다면 기기 관리 정책으로 잠긴 것입니다. IT 부서에 문의하거나 Cisco, OpenVPN, 사설망 클라이언트를 대신 쓰세요.

## Linux

1. Hiddify 페이지의 다운로드 영역에서 .deb를 받아 더블클릭해 소프트웨어 센터로 설치하거나, 다운로드 폴더에서 터미널을 열고 다음을 실행합니다(Debian, Ubuntu와 그 파생 배포판).

```bash
sudo apt install ./downloaded-file-name.deb
```

2. 설치 직후 바로 연결하면 'operation not permitted'가 나오고 VPN 모드가 켜지지 않습니다. 공식 deb는 설치해도 이 권한이 없기 때문입니다. 터미널을 열어 아래 명령으로 Hiddify에 권한을 준 뒤 Hiddify를 다시 엽니다.

```bash
echo /usr/share/hiddify/lib | sudo tee /etc/ld.so.conf.d/hiddify.conf && sudo ldconfig && sudo setcap cap_net_admin,cap_net_raw+ep /usr/share/hiddify/hiddify
```

3. **Hiddify를 업데이트할 때마다 다시 실행하세요**: 권한은 프로그램 파일에 붙어 있는데, 업데이트하면 파일이 교체되어 권한이 사라집니다.

deb 패키지는 x64용입니다. ARM Linux 기기에서는 OpenVPN을 쓰면 되고, 같은 계정으로 됩니다.

## Android

1. Hiddify 페이지의 다운로드 영역에서 .apk를 받습니다. 페이지가 휴대폰에 맞는 아키텍처를 자동으로 추천하며, 대부분의 휴대폰은 ARM64입니다. Google Play를 쓸 수 있다면 스토어에서 바로 설치해도 됩니다.
2. 설치 중 '출처를 알 수 없는 앱' 관련 안내나 보안 앱의 경고가 나오면 허용합니다.
3. 처음 연결을 누르면 시스템이 VPN 권한을 요청합니다. 허용을 누르세요.

## iPhone / iPad

1. App Store에서 'Hiddify'를 검색해 설치합니다. 무료입니다.
2. 찾을 수 없거나 '이 앱은 현재 사용자의 국가 또는 지역에서 사용할 수 없습니다'라는 메시지가 뜨면: iOS에서는 중국 외 지역 Apple ID로 App Store에서 설치해야 합니다(Hiddify는 미국, 홍콩, 대만, 일본, 싱가포르 스토어에 있습니다). 새 계정을 만드는 것을 권합니다. App Store에서 아무 무료 앱의 '받기' → '새로운 Apple 계정 만들기'를 누르고, 지역은 홍콩이나 미국 등을, 결제 수단은 '없음'을 고르세요. 계정은 App Store에서만 바꾸며 iCloud에는 영향이 없습니다. 전체 단계는 [06 · iOS에서 앱을 설치할 수 없을 때](06-ios-app-store.md)를 보세요.
3. 처음 연결을 누르면 시스템이 VPN 권한을 요청합니다. 허용을 누르세요.

남이 공유해 준 Apple ID는 **쓰지 마세요**. 그 사람이 원격으로 기기를 잠글 수 있습니다.

## 설치 후: 구독을 가져와 연결하기

1. 웹사이트에 로그인해 Hiddify 페이지를 엽니다.
2. 원하는 지역의 국기를 누르면 QR 코드가 뜹니다. 또는 페이지 위쪽의 '모든 지역 가져오기 · 자동 선택'을 누르면 중국 외 모든 지역을 한 번에 가져와 클라이언트가 자동으로 고르게 할 수 있습니다. **중국 지역은 따로 가져옵니다**: 해외에서 중국 동영상을 보거나 중국 인터넷 뱅킹을 쓰려면 중국 국기를 눌러 가져오세요.
3. QR 코드 아래에는 구독 형식별로 나뉜 버튼 세 개가 있습니다. Hiddify는 첫 번째 버튼(Hiddify / sing-box / GUI.for.SingBox / Karing이라고 적혀 있고 부제는 'sing-box 구독')을 쓰며, 휴대폰과 컴퓨터 모두 같은 버튼입니다. 휴대폰: 누른 뒤 Hiddify로 전환해 안내대로 추가하거나, 다른 기기의 Hiddify로 코드를 스캔합니다. 컴퓨터: 누르면 https:// 주소가 복사되니, Hiddify에서 '+' → 'Add from clipboard'(클립보드에서 추가)를 누릅니다.
4. 연결을 누릅니다.

세 버튼의 차이, Clash 등 다른 클라이언트로 가져오는 법, 구독이 만료되는지는 [02 · 구독 링크 가져오는 법(Hiddify, Clash, Shadowrocket)](02-singbox-subscription-links.md)을 보세요. 가져왔는데 연결되지 않으면 [문제 해결 04](../troubleshooting/04-singbox-import-not-connecting.md)를 보세요.

## 자주 묻는 질문

**설치 파일을 수정했나요?** 아닙니다. 데스크톱 설치 파일은 Hiddify 공식 릴리스 패키지를 그대로 옮긴 미러입니다. Hiddify 페이지의 각 줄에 공식 릴리스 페이지 링크가 있으니 직접 버전을 비교할 수 있고, 파일을 VirusTotal에 올려 한 번 더 확인할 수도 있습니다.


**Mac에서 xattr 명령을 이미 실행했는데 여전히 연결되지 않아요.** '네트워크 확장 프로그램'이 승인되지 않았을 가능성이 큽니다. 위 macOS 항목대로 시스템 설정에서 Hiddify 스위치를 켜세요.

**Linux에서 Hiddify를 업데이트했더니 VPN 모드가 다시 안 돼요.** 정상입니다. 업데이트 후 권한 부여 명령을 한 번 더 실행하세요.

**ARM 기반 Windows나 Linux 컴퓨터에서도 쓸 수 있나요?** 쓸 수 있습니다. OpenVPN 같은 다른 연결 방식을 쓰면 되고 같은 계정으로 됩니다. Hiddify 데스크톱 패키지는 현재 x64용입니다.

**허용하는 과정이 번거로운가요?** Cisco(Cisco Secure Client), OpenVPN(OpenVPN Connect), 사설망(Tailscale)은 모두 더블클릭하면 바로 열립니다. 백신 프로그램이 막지 않고 Mac에서도 '손상되었다'는 메시지가 뜨지 않으며, 계정도 같은 것을 씁니다.

## 더 읽을거리

- [Hiddify 페이지: 클라이언트 다운로드와 지역별 QR 코드](https://www.leotun.com/ko/singbox?utm_source=github&utm_content=client-09)
- [구독 링크 가져오는 법(Hiddify, Clash, Shadowrocket)](https://www.leotun.com/ko/guides/singbox-subscription?utm_source=github&utm_content=client-09)
- [백신이 클라이언트를 막거나 Mac에서 손상되었다고 할 때: 먼저 확인하고 허용하기](https://www.leotun.com/ko/guides/antivirus-false-positive?utm_source=github&utm_content=client-09)
- [macOS '네트워크 확장 프로그램' 승인이란 무엇이고 어떻게 허용하나](https://www.leotun.com/ko/guides/macos-network-extension?utm_source=github&utm_content=client-09)
- [iOS에서 앱을 설치할 수 없을 때](https://www.leotun.com/ko/guides/ios-app-store?utm_source=github&utm_content=client-09)

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=client-09) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=client-09)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 4시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 15크레딧(개인 요금제로 약 15일)을 받으며 상시 진행하는 혜택입니다
