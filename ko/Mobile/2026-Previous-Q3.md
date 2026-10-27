2026년 3분기(7~9월)에 정식 게재된 학회 및 저널 논문 가운데 모바일 분류에 해당하는 논문 7편을 정리했습니다. 프리프린트(arXiv, IACR ePrint)는 제외했습니다.

- 프라이버시 (3)
- 그 외 (4)

---

**세부 분류: 프라이버시**

# Bridges to Self: Silent Web-to-App Tracking on Mobile via Localhost
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

브라우저와 모바일 운영체제는 샌드박싱과 프로세스 격리로 웹과 앱 맥락을 분리하지만, 이 논문은 Android에서 Meta와 Yandex가 실제로 그 격리를 깨고 웹 추적을 네이티브 신원과 연결했음을 보입니다. HTTP(S), WebSocket, WebRTC 같은 웹 표준을 이용해 localhost에서 모바일과 웹 맥락을 잇고, 가명 웹 쿠키를 오래 유지되는 네이티브 사용자 ID에 연결해 지속적이고 은밀한 교차 맥락 추적과 비식별화 해제를 가능하게 합니다. 이 기법은 쿠키 삭제, 시크릿 모드, 광고 ID 재설정, VPN, 업무/개인 프로필 분리를 모두 무력화합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/vlummens

### Contribution
- localhost를 매개로 한 웹-앱 추적이라는, 그동안 기록되지 않은 추적 방식을 미국·EU 대규모 웹 크롤과 Android 앱 분석으로 규명했습니다.
- Meta Pixel과 Yandex Metrica가 쿠키 동의 배너를 받기 전에 localhost 브리징을 시작했음을 보였습니다.
- 책임 있는 공개 이후 브라우저의 패치와 Local Network Access(LNA) 권한을 평가하고, WebRTC의 전역 유니캐스트 IPv6와 *.local mDNS 조회를 통한 추가 우회 채널까지 찾아냈습니다.

### Evaluation
- 미국과 EU 관측점에서의 대규모 웹 크롤과 체계적 Android 앱 분석을 결합해, 실제로 작동하는 추적 채널을 측정했습니다.
- 법적 분석을 함께 실어 플랫폼과 브라우저의 격리 원칙, 위협·신뢰 모델, 프로토콜 표준, 앱 심사 과정을 재검토해야 한다고 주장합니다.
- 측정 시점의 특정 추적기(Meta, Yandex) 동작에 기반하므로, 공개 이후 해당 동작은 중단되거나 바뀌었을 수 있습니다.

#### Comment
- 모바일에서 웹과 앱의 신원이 localhost로 연결된다는 점은, 앱 내 WebView와 SDK가 만드는 추적면을 보는 모바일 보안 관점에서 매우 중요한 사례입니다.
- KU 뢰번, IMDEA Networks, 라드바우드대 공동 연구이며 공개 PDF를 갖춘 USENIX Security 게재 논문입니다.

---

# Health Hazard, Handle with Care: Investigating the Privacy Risks of Android's Health Connect
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

Android의 Health Connect는 여러 앱이 건강·피트니스 데이터를 공유하도록 중개하는 플랫폼입니다. 이 논문은 앱이 자신이 만들지 않은 다른 앱의 건강 기록에 접근하는 실태와, 그 접근이 앱의 데이터 안전(Data Safety) 공시와 어긋나는 지점을 조사해 프라이버시 위험을 분석합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/spyridakis

### Contribution
- Health Connect를 매개로 한 앱 간 건강 데이터 접근의 프라이버시 위험을 체계적으로 조사했습니다.
- 다른 앱이 만든 기록에 접근하면서 이를 데이터 안전 섹션에 공시하지 않는 불일치를 드러냈습니다.

### Evaluation
- 분석 대상 앱의 28.49%(100개)가 다른 앱이 만든 기록 2,334건에 접근했고, 그중 25개는 해당 수집을 데이터 안전 공시에 밝히지 않았습니다.
- 앱의 15.67%가 자신의 것이 아닌 기록을 최소 5건, 10%가 최소 20건 접근했습니다. 실제 앱 측정에 기반해 근거가 구체적입니다.

#### Comment
- 건강 데이터 중개 플랫폼에서 공시와 실제 접근의 괴리를 보여, 모바일 프라이버시와 민감 데이터 접근 통제를 다루는 입장에서 참고가 됩니다.
- 크레타공대, 일리노이대 시카고, 키프로스공대 공동 연구이며 USENIX Security 게재 논문입니다.

---

# Plain Text, Plain Risks: Measuring HTTP Inclusion in Android WebViews at Scale
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

HTTPS 확산과 브라우저의 시각적 경고로 전통적 웹에서는 중간자 공격이 크게 줄었지만, 모바일은 사정이 다릅니다. Android WebView로 임베드된 웹 콘텐츠는 이런 보호가 약합니다. 이 논문은 WebView의 HTTP 콘텐츠 처리를 현대 모바일 브라우저와 비교하고, 대규모로 HTTP 포함 실태를 측정합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/beer

### Contribution
- Android WebView의 HTTP 처리를 모바일 브라우저와 비교해 여러 보안 미비점을 드러냈습니다.
- WebView의 HTTP 트래픽과 설정을 체계적으로 탐지하는 정적-동적 분석 파이프라인 WebViewTrace를 개발했습니다.
- 18만여 개 앱을 대상으로 WebView 내 HTTP 콘텐츠를 처음으로 대규모 실증 분석했습니다.

### Evaluation
- 189,779개 앱을 분석해, 모든 HTTP 트래픽을 허용하는 앱의 69.96%가 혼합 콘텐츠 정책(MCP)까지 완화한다는 보안 다운그레이드 경향을 정량화했습니다.
- 인기 앱 사례 연구로 UI 스푸핑부터 앱 완전 장악까지의 공격 벡터를 보였고, 개발자 40명을 대상으로 한 질적 연구에서 보안 다운그레이드가 오해, 호환성 요구, 제3자 SDK 요구에서 비롯됨을 확인했습니다.
- 대규모 측정과 개발자 조사를 함께 갖춰 근거가 탄탄합니다.

#### Comment
- WebView의 HTTP 허용과 혼합 콘텐츠 완화가 만드는 공격면은, 앱 내 WebView 보안과 SDK가 강제하는 설정을 다루는 입장에서 직접적인 참고가 됩니다.
- TU 빈과 바이로이트대 공동 연구이며 USENIX Security 게재 논문입니다.

---

**세부 분류: 그 외**

# "Tap" Without Tapping: A Tag Discovery Forgery Attack on Android NFC
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

탭투페이처럼 NFC 태그를 탭해 로직을 시작하는 Tap-to-X 앱은 탭을 사용자의 근접과 의도의 증거로 여깁니다. Android에서는 운영체제가 태그 데이터를 읽어 적절한 앱에 전달하는데, 이 탭 이후의 디스패치 과정의 보안은 거의 연구되지 않았습니다. 이 논문은 디스패치 과정의 두 가지 운영체제 수준 설계 약점이 의미적 출처 간극을 만들어, 로컬 악성 앱이 실제 NFC 상호작용 없이 물리적 탭을 흉내 낼 수 있음을 보입니다. 이를 이용한 태그 디스패치 위조 공격(TDFA)은 알리페이, 화웨이 AI Life, 삼성 갤럭시 웨어러블 등 실제 앱에 영향을 줍니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/li-yilin

### Contribution
- Android의 탭 이후 태그 디스패치 과정을 분석해, 물리적 탭 없이 탭을 위조하게 하는 두 가지 설계 약점을 규명했습니다.
- 운영체제 수준의 근본 수정안을 제시하고, 그 전까지 쓸 수 있는 앱 개발자용 완화 지침을 제공합니다.

### Evaluation
- Google Play 앱 76,333개를 대규모 분석해 외부에서 시작 가능한 RW 핸들러를 가진 잠재 영향 앱 601개를 찾았고, 설치·시험 가능한 597개 중 498개에서 위조 전달 성공을 기기에서 확인했습니다.
- Android 보안팀, 알리페이, 화웨이에 책임 있게 공개해 확인을 받았고, Google이 CVE-2026-0081을 부여했으며 버그 바운티도 수령했습니다.
- 대규모 측정과 실기기 검증을 함께 갖춰 판단 근거가 탄탄합니다.

#### Comment
- NFC 탭이 결제·인증의 의도 증거로 쓰이는 모바일 환경에서, 운영체제의 디스패치 설계가 위조 가능하다는 점은 탭 기반 보안 흐름 설계에 직접적인 함의가 있습니다.
- 중국 기관 검증: 산둥대 주도이며 사이먼프레이저대, 홍콩시티대가 참여한 공동 연구입니다. CVE 부여와 벤더 확인, 공개 아티팩트(Zenodo)로 외부 검증이 이뤄졌고 실기기 결과가 구체적이라 포함했습니다.

---

# Cracks in the Walled Garden: Dissecting the Gray-Market of Unauthorized iOS App Distribution via Ad Hoc Sideloading
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

Apple은 엄격한 코드 서명을 강제하고 공식 App Store를 통한 배포를 요구하지만, 개발자 테스트용으로 설계된 Ad Hoc 프로비저닝이 비인가 앱 배포 통로가 됐습니다. 개인 개발자 인증서와 사용자 측 서명을 이용해 심사를 우회하는 이 관행은, 인증서 재판매와 제3자 서명 도구, 서명되지 않은 .ipa 배포를 잇는 구조화된 회색 시장으로 발전했습니다. 이 논문은 특히 중국의 통합 서비스 운영에 초점을 맞춰 이 시장을 처음으로 체계적으로 분석합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/liu-yijing

### Contribution
- Ad Hoc 사이드로딩 기반 비인가 iOS 앱 배포 회색 시장을 처음으로 체계적으로 조사했습니다.
- 인증서 재판매(최대 3,000% 마진)로 이어지는 다층 인증서 유통 모델과 서명 도구가 쓰는 공통 수법을 밝혔습니다.
- 배포 앱 대부분이 동적 라이브러리 주입으로 기능을 바꾼 정식 앱의 변형판이며, 이것이 앱과 시스템 보호를 무력화해 사용자를 위험에 노출한다는 점을 보였습니다.

### Evaluation
- 사용자 중심 수집으로 인증서 교환용 활성 서명 사이트 3,359개를 식별하고, 서명 도구 12종을 역공학했으며, 배포된 .ipa 항목 8,216개를 확보했습니다.
- 실제 시장 데이터를 폭넓게 수집해 분석 근거가 구체적이며, 중국 중심 시장이라는 범위를 명시합니다.

#### Comment
- iOS 코드 서명과 동적 라이브러리 주입, 앱 변조를 정면으로 다뤄, iOS 보안 SDK와 무결성·런타임 보호를 설계하는 입장에 매우 직접적인 사례입니다. 사용자 관심사인 iOS 바이너리 보호와 맞닿아 있습니다.
- 중국 기관 검증: 칭화대와 BNRist의 연구(류바이쥔, 두안하이신 등)로, 네트워크·생태계 측정 분야 최상위 실적이 꾸준한 연구실입니다. 공개 아티팩트(Zenodo)와 구체적 수집 방법으로 재현 가능해 포함했습니다. USENIX Security 게재 논문입니다.

---

# Raising the Flag: Detecting Missing Permission Controls in Mini-Program APIs
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

슈퍼앱의 미니프로그램은 운영체제처럼 민감한 기능에 접근하는 API를 제공받습니다. 이 논문은 미니프로그램 API에서 권한 통제가 빠진 지점을 탐지하는 문제를 다룹니다. 어떤 API가 권한 검사를 거쳐야 하는데 그러지 않는지를 찾아내, 비인가 접근으로 이어질 수 있는 결함을 드러냅니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/wei-zhiao

### Contribution
- 미니프로그램 API에서 누락된 권한 통제를 탐지하는 방법을 제안해, 슈퍼앱 플랫폼이 제공하는 API 수준의 인가 결함을 체계적으로 찾습니다.
- 권한 검사가 있어야 할 API와 실제 검사 여부를 비교해 결함 후보를 도출합니다.

### Evaluation
- (전문을 받았으나 요약 다이제스트에서 세부 수치가 충분히 추출되지 않았습니다. 평가는 미니프로그램 API 집합에 대한 분석과 발견된 결함 검증으로 구성됩니다.)
- 실제 플랫폼 API를 대상으로 한 분석이라 근거가 구체적이며, 세부 수치는 원문 확인을 권합니다.

#### Comment
- 슈퍼앱이 인증은 제공하되 인가를 API 구현에 맡기는 구조의 결함을 다뤄, 1분기의 app-in-app 클라우드 자원 연구(NDSS 2026)와 함께 미니프로그램 생태계 보안의 반복되는 주제를 보여 줍니다.
- 워털루대, 오하이오주립대, 일리노이대 어배너-섐페인 공동 연구이며 USENIX Security 게재 논문입니다.

---

# SoK: History Doesn't Repeat Itself, but Android Design-Level Vulnerabilities Rhyme in OpenHarmony
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

이 체계화(SoK) 논문은 Android에서 오랫동안 알려진 설계 수준 취약점이 신흥 모바일 운영체제 OpenHarmony에서 어떻게 비슷한 형태로 되풀이되는지를 정리합니다. 두 운영체제의 설계를 비교해, 플랫폼이 바뀌어도 같은 범주의 설계 결함이 재현된다는 점을 보입니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/chen-hongkai

### Contribution
- Android의 설계 수준 취약점 범주를 체계화하고, 이를 OpenHarmony에 대응시켜 신흥 운영체제에서의 재현 양상을 분석합니다.
- 플랫폼 간에 반복되는 설계 결함의 공통 원인을 정리해 방어 설계의 교훈을 제시합니다.

### Evaluation
- Android와 OpenHarmony의 설계를 대조하는 체계화 연구로, 알려진 취약점 범주를 기준으로 두 플랫폼을 비교합니다.
- 새로운 공격의 성공률 같은 실측보다는, 설계 결함의 분류와 재현 양상 정리에 초점을 둡니다.

#### Comment
- OpenHarmony가 확산하는 흐름에서 Android의 설계 교훈이 어디까지 이어지는지 보여, 다중 플랫폼 모바일 보안 SDK를 설계하는 입장에 유용한 참고가 됩니다. 특정 세부 분류에 들지 않아 그 외로 넣었습니다.
- 애리조나주립대, CISPA, 오하이오주립대 공동 연구이며 USENIX Security 게재 논문입니다.
