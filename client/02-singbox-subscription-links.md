# 02 · 구독 링크 가져오는 법(Hiddify, Clash, Shadowrocket)

> 웹사이트 버전(더 자세함): https://www.leotun.com/ko/guides/singbox-subscription?utm_source=github&utm_content=client-02

프록시 회선 업체(구독형 프록시를 파는 곳)가 주는 '구독 링크'는 클라이언트가 전체 설정을 내려받는 HTTPS 주소일 뿐입니다. 서버, 포트, 인증 정보가 모두 들어 있어 손으로 입력할 것이 없습니다. LeoTun의 Hiddify 페이지도 같은 것을 주는데, 처음부터 세 가지 형식으로 주기 때문에 Hiddify, Clash, Shadowrocket이 각자 자기 것을 가져가면 되고 변환할 필요가 없습니다.

## 팝업의 버튼 세 개

웹사이트 로그인 → Hiddify 페이지 → 지역 국기를 누르면 QR 코드가 뜨고 그 아래에 버튼 세 개가 있습니다. 버튼은 운영체제가 아니라 **구독 형식별로** 나뉘어 있어서 휴대폰과 컴퓨터에 같은 버튼이 보입니다.

| 버튼에 적힌 클라이언트 | 부제 | 누르면 복사되는 것 |
|---|---|---|
| Hiddify / sing-box / GUI.for.SingBox / Karing | sing-box 구독 | 휴대폰에서는 앱을 실행하는 `sing-box://import-remote-profile?url=…` 가져오기 링크, 컴퓨터에서는 붙여 넣을 일반 `https://…` 설정 URL. 설정에 라우팅 규칙과 IPv6 차단 규칙이 이미 들어 있어 '구독 템플릿'으로 감쌀 필요가 없습니다 |
| Clash Meta / Clash Verge / FlClash / Stash / Mihomo Party / Clash Nyanpasu / ClashX Meta / OpenClash | Clash 구독 | Clash 형식(YAML) 구독 URL. 클라이언트의 구독 / 프로필 목록에 붙여 넣습니다 |
| NekoBox / Shadowrocket / v2rayN / v2rayNG / Streisand / V2Box / Loon / Egern / Husi / NekoRay / Pharos Pro / Bedlam / Furious / daed / Lumen KVN / Kitty Pro | 공유 링크 | `hysteria2://…` 한 줄. 노드만 담겨 있고 라우팅 규칙은 없습니다 |

- 이름이 한 줄에 다 들어가지 않으면 반복해서 흘러가며 보이는데, 정상입니다.
- **버튼을 누르면 위의 QR 코드도 그 형식으로 바뀌어** 해당 클라이언트가 스캔할 수 있습니다. 팝업을 처음 열었을 때 QR 코드는 Hiddify / sing-box용이라, 다른 클라이언트로 바로 스캔하면 'Invalid QR code'(잘못된 QR 코드)가 뜹니다. 먼저 내 클라이언트의 버튼을 누른 뒤 스캔하거나 붙여 넣으세요.
- 페이지 위쪽의 '모든 지역 가져오기 · 자동 선택' 팝업에는 앞의 두 버튼만 있고 공유 링크는 없습니다.

**구독 변환**: 한 형식을 다른 형식으로 바꿔 주는 외부 웹사이트입니다. LeoTun은 세 형식을 모두 직접 주므로 **변환할 필요가 없습니다.** 인증 정보가 든 링크를 변환 사이트에 넘기는 것은 계정을 제3자에게 넘기는 것과 같으니 하지 마세요.

## Hiddify / sing-box 계열: 첫 번째 버튼

1. Hiddify를 설치합니다(Android: 웹사이트 다운로드 페이지나 Google Play, iOS: App Store, 데스크톱 앱은 Windows / macOS / Linux 지원). sing-box 코어가 내장되어 있습니다.
2. 지역 국기를 누르면 QR 코드가 뜹니다.
3. 휴대폰: 첫 번째 버튼을 누르고 Hiddify로 전환하면 클립보드에서 추가하라는 안내가 나옵니다. 또는 다른 기기의 Hiddify에서 'Scan QR code'(QR 코드 스캔)를 씁니다. 컴퓨터: 같은 버튼을 누르면 https:// 주소가 복사되니, Hiddify에서 '+' → 'Add from clipboard'(클립보드에서 추가)를 누르고 저장합니다.
4. 연결을 누르고, 처음에는 VPN 권한을 허용합니다. 지역을 추가하려면 다른 국기를 누르세요. 지역마다 별도 프로필입니다.

## Clash 계열: 두 번째 버튼

Clash Meta(mihomo), Clash Verge, FlClash, Stash 등은 'Clash 구독' 버튼을 누르고 복사된 URL을 클라이언트의 구독 / 프로필 목록에 붙여 넣으면 됩니다. 구독 변환기는 필요 없습니다.

**Clash 계열 클라이언트는 공유 링크를 쓰면 안 됩니다.** `hysteria2://` 한 줄을 프로필로 가져올 수 없습니다.

## 그 밖의 클라이언트: 세 번째 버튼

'공유 링크' 버튼을 누른 뒤 NekoBox / Shadowrocket / v2rayN / v2rayNG 등에서 '클립보드에서 가져오기'를 쓰거나, 버튼을 누른 뒤 위의 QR 코드를 스캔하세요. 공유 링크에는 규칙이 없으므로 라우팅과 IPv6는 직접 설정해야 합니다. 해외에서 중국 콘텐츠를 보려면 중국 도메인을 노드로 보내고 IPv6를 끄세요.

버튼에서 v2rayN 뒤에 나열된 클라이언트는 모두 hysteria2를 지원하지만, 공유 링크는 hysteria2의 확장 형식을 써서 일부 클라이언트는 해석하지 못합니다. 가져오기가 실패하거나 연결되지 않으면 Hiddify로 바꾸세요.

## 쓸 수 없는 클라이언트

| 클라이언트 | 이유 |
|---|---|
| Surge | hysteria2를 지원하지만 자체 설정 형식만 읽어서 세 형식 모두 맞지 않습니다 |
| Quantumult X | 이 종류의 회선을 지원하지 않습니다 |
| 원조 Clash, Clash for Windows | 코어에 hysteria2가 없습니다. mihomo 코어 클라이언트를 쓰세요 |

## 구독은 만료되나요?

- **시간이 지나도 만료되지 않습니다.** 구독 URL 속 토큰은 계정에 묶여 있어 계정이 유효한 동안 계속 작동합니다. 연장하거나 요금제를 바꿔도 다시 가져올 필요가 없습니다.
- **비밀번호를 바꾸면 예전 URL은 즉시 무효가 됩니다.** 휴대폰을 잃어버리거나 링크가 새었을 때 접근을 끊는 방법이 이것입니다. 바꾼 뒤에는 코드를 다시 스캔하세요.
- **계정이 만료되면** URL이 401을 돌려줍니다. 연장하면 기존 프로필을 바꿀 필요가 없습니다.
- **2026년 9월 이전에 가져온 프로필**에는 IPv6 차단 규칙이 없으니 지우고 다시 가져오세요.

가져왔는데 연결되지 않으면 [문제 해결 04](../troubleshooting/04-singbox-import-not-connecting.md)를 보세요.

## 자주 묻는 질문

**Hiddify 구독과 Clash 구독은 무엇이 다른가요?** 형식이 다르고(JSON과 YAML), 각 클라이언트는 상대 형식의 구독을 알아보지 못하지만, 노드 자체는 양쪽에서 다 쓸 수 있습니다. LeoTun은 둘 다 직접 줍니다. Clash 계열 클라이언트는 'Clash 구독' 버튼을 누르고, 공유 링크는 쓰면 안 됩니다.

**프로필 하나에 모든 지역을 넣을 수 있나요?** 국기로 가져오면 지역마다 프로필이 하나씩 생기고, 클라이언트의 프로필 목록에서 바꿔 가며 씁니다. 그래야 한 지역의 주소가 바뀌어도 그 지역에만 영향이 갑니다. 중국 밖 모든 지역을 한 번에 가져와 클라이언트가 자동으로 고르게 하려면 페이지 위쪽의 '모든 지역 가져오기 · 자동 선택'을 누르세요(sing-box 구독과 Clash 구독 버튼만 있습니다).

**QR 코드를 가족에게 보내도 되나요?** QR 코드에는 계정 인증 정보가 들어 있어서, 보낸 사람이 내 계정을 갖게 됩니다. 가족과 나눠 쓰는 것은 괜찮지만(동시 접속 기기는 요금제별로 개인 2대, 패밀리 4대, 기업 8대) 공개된 곳에 올리지는 마세요. 새었다면 비밀번호를 바꾸면 무효가 됩니다.

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=client-02) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=client-02)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 4시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 개인 요금제 20일을 받으며 상시 진행하는 혜택입니다
