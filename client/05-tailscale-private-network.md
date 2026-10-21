# 05 · 사설망(Tailscale): 설치, 이 사이트의 컨트롤 서버로 로그인, 출구 고르기

> 웹사이트 버전(더 자세함): https://www.leotun.com/ko/guides/tailscale-mesh?utm_source=github&utm_content=client-05

사설망 메뉴는 Tailscale(WireGuard 기반의 네트워크 도구)을 씁니다. LeoTun이 자체 컨트롤 서버를 운영하므로 **이 사이트의 계정**으로 로그인하며, Tailscale 공식 계정과는 관계가 없습니다. 한 번 로그인하면 계속 온라인 상태이고, 출구 지역은 메뉴에서 언제든 바꿀 수 있습니다. VPN과 무엇이 다르고 누구에게 맞는지는 [네트워크 가이드 03](../network/03-private-network-vs-vpn.md)을 보세요.

## 설치

| 플랫폼 | 받는 곳 |
|---|---|
| Windows / macOS / Linux / Android | [웹사이트 사설망 페이지](https://www.leotun.com/ko/mesh?utm_source=github&utm_content=client-05)의 다운로드 영역(이 사이트에서 바로 받을 수 있어 공식 사이트에 갈 필요가 없습니다) |
| iPhone / iPad | App Store. 중국 외 지역 Apple ID가 필요합니다([클라이언트 06](06-ios-app-store.md) 참고) |

## 로그인

1. **먼저 공식 계정에서 로그아웃합니다**(로그인한 적이 있다면). 휴대폰은 프로필 사진 → Log Out(로그아웃), 컴퓨터는 `tailscale logout`을 실행합니다. 완전히 로그아웃하지 않으면 다음 단계에 필요한 항목이 나타나지 않습니다.
2. **로그인 대상을 이 사이트로 지정합니다**:
   - 휴대폰: 로그아웃된 화면 오른쪽 위의 '⋯' → Use custom server(사용자 지정 서버. 버전에 따라 Use an alternate server)를 누르고, 웹사이트 사설망 페이지에 나온 주소를 입력한 뒤 Log in(로그인)을 누릅니다.
   - Windows / Linux: 웹사이트 페이지에서 `tailscale up --login-server=…` 명령을 복사해 PowerShell / 터미널에서 실행합니다.
   - macOS: **Log in을 누르지 마세요.** Tailscale 창에서 계정 줄의 화살표 → Account Settings… → Accounts → 'Add Account…' 옆의 작은 화살표 → Add Account Using Alternate Server(다른 서버로 계정 추가)를 누르고, 주소를 붙여 넣은 뒤 Add Account…를 누릅니다.
3. 브라우저가 이 사이트의 로그인 페이지를 자동으로 엽니다. 이 사이트 계정으로 확인하고 클라이언트로 돌아오면 이미 온라인 상태입니다.

## 출구 고르기

- 휴대폰: 메뉴 → Exit Node(출구 노드)에서 지역을 고르면 바로 적용됩니다.
- 컴퓨터: 트레이 / 메뉴 막대 아이콘 → Exit Node 하위 메뉴. 또는 `tailscale set --exit-node=<region-name>`(쓸 수 있는 목록은 `tailscale exit-node list`로 확인).
- 출구를 쓰지 않으려면 None(없음)을 고릅니다(명령줄에서는 등호 뒤를 비워 둡니다). 출구는 한 번에 하나만 쓸 수 있습니다.

## 만료와 기기 수

- 기기의 로그인 유효 기간은 계정 만료일을 따르며, 만료되면 몇 분 안에 오프라인이 됩니다. 연장한 뒤 로그인을 한 번 다시 하면 되고, 다시 설치할 필요는 없습니다.
- 동시에 접속할 수 있는 기기 수는 요금제에 따라 다르고(개인 2대, 패밀리 4대, 기업 8대) 다른 접속 방식과 한도를 함께 씁니다. 요금제 한도를 넘으면 계정 유형을 잠시 올렸다가(남은 기간은 가격 기준으로 같은 가치로 환산) 끝나면 되돌리면 됩니다.

## 다른 방식이 맞는 두 경우

- 같은 기기에서 다른 VPN(회사 AnyConnect, 다른 메시 네트워크 소프트웨어)이 돌고 있을 때: DNS와 라우팅을 두고 서로 다툽니다. 중국 동영상을 볼 때 저작권 안내가 뜨거나 회사 인트라넷이 안 열리는 원인이 바로 이것입니다.
- UDP를 제한하는 학교 / 회사 네트워크에서: WireGuard는 UDP 위에서 동작하므로 Tailscale의 릴레이를 거칠 수밖에 없어 매우 느립니다. AnyConnect로 바꾸세요.

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=client-05) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=client-05)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 4시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 개인 요금제 20일을 받으며 상시 진행하는 혜택입니다
