# 01 · 해외 IP가 필요한 서비스와 회선의 작동 방식

기준은 해외에서 중국에 접속할 때와 정반대입니다. 서비스가 내 출발지 IP가 중국 본토라는 것을 알아채거나 그 서버에 아예 닿지 못하면, 열리지 않거나 기능이 줄거나 극도로 느려집니다. 아래 표는 용도별로 정리했습니다.

| 분류 | 예 | 회선 없이 쓰면 | IP 말고 필요한 것 |
|---|---|---|---|
| 업무 | Google Workspace, Slack, Zoom, Teams, Notion | 열리지 않거나 계속 끊김 | 회사 계정 |
| 개발 | GitHub, npm, Docker Hub, 미러가 아닌 PyPI 소스, Stack Overflow | 너무 느려 시간 초과 | 없음 |
| AI | ChatGPT, Claude, Gemini | 열리지 않음 | 계정 가입 국가, 전화번호 |
| 연구 | Google Scholar, 논문 데이터베이스, 대학 이메일 | 열리지 않거나 극도로 느림 | 대학 계정 |
| 게임 | Steam 해외 지역, PSN, Switch eShop, 해외 서버 | 스토어가 열리지 않고 지연이 큼 | 해당 지역 서버용 계정 |
| 동영상·음악 | YouTube, Netflix, Disney+, Spotify | 열리지 않음 | 유료 계정, 그리고 계정 지역이 IP와 맞아야 함 |
| 소셜 | X, Instagram, Telegram, Discord, WhatsApp | 열리지 않음 | 전화번호 |

## 꼭 구분할 점

**'해외 IP가 필요한 것'과 '해외 계정이 필요한 것'은 별개입니다.** GitHub와 YouTube는 IP만 바꾸면 되지만, Netflix는 지역이 맞는 유료 계정이 필요하고, ChatGPT에 가입하려면 인증 코드를 받을 수 있는 해외 전화번호가 필요합니다. 회선이 해결하는 것은 '열리느냐'이고, 계정은 각자 준비해야 합니다.

## 회선의 작동 방식

내 트래픽은 먼저 암호화되어 해외 서버로 가고, 그 서버가 목적지에 대신 접속합니다. 목적지에 보이는 것은 그 서버의 IP입니다. 방법은 세 가지로, 클라이언트, 웹 프록시, 공유기가 있습니다. 고르는 법은 [상황별로 어떤 연결 방식이 맞을까](../network/02-choose-your-connection-method.md)를 보세요.

## 흔한 오해 세 가지

- **DNS를 바꿔도 소용없습니다.** 연결이 안 되는 것은 경로 문제이지 이름 풀이 문제가 아닙니다.
- **속도는 두 지점 사이의 회선에 달려 있습니다.** 중국에서 밖으로 나갈 때 병목은 국경 간 구간과 통신사의 출구이므로, 서버 사양보다 지역 선택이 더 중요합니다. [03](03-which-region-is-fastest.md)을 보세요.
- **중국 앱을 쓰는 동안 모든 것이 회선을 거칠 필요는 없습니다.** 분할 라우팅을 켜세요. 기본으로 차단된 사이트만 회선을 거치고, 중국 사이트와 중국에서도 원래 잘 열리는 해외 사이트는 직접 연결되어 어느 쪽도 돌아가지 않습니다. [공유기 분할 라우팅](../router/03-router-split-routing.md)을 보세요.

---
[LeoTun](https://www.leotun.com/ko?utm_source=github&utm_content=overseas-access-01) 팀 작성 · 궁금한 점은 [문의 페이지](https://www.leotun.com/ko/contact?utm_source=github&utm_content=overseas-access-01)를 보세요(그룹, 이메일, 고객 지원이 모두 나와 있습니다) · 가입하면 4시간 무료 체험, 초대한 친구가 결제하면 두 사람 모두 15크레딧(개인 요금제로 약 15일)을 받으며 장기간 유효합니다
