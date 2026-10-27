2026년 1분기(1~3월)에 정식 게재된 학회 및 저널 논문 가운데 모바일 분류에 해당하는 논문 18편을 정리했습니다. 프리프린트(arXiv, IACR ePrint)는 제외했습니다.

- 악성코드 및 분석 (1)
- 온디바이스 LLM (1)
- 프라이버시 (7)
- TEE 및 사이드 채널 (2)
- 그 외 (7)

---

**세부 분류: 악성코드 및 분석**

# CHAMELEOSCAN: Demystifying and Detecting iOS Chameleon Apps via LLM-Powered UI Exploration
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

App Store 심사를 통과할 때는 평범한 앱처럼 보이다가, 개발자가 비공식 경로로 알려 준 특정 조작을 하면 도박이나 불법 서비스 앱으로 바뀌는 iOS 카멜레온 앱을 다룹니다. 이 논문은 이런 앱의 변신 방식을 대규모로 분석해 10가지 범주로 분류하고(그중 4가지는 처음 보고), 탐지 시스템 CHAMELEOSCAN을 제안합니다. CHAMELEOSCAN은 App Store 메타데이터와 사용자 리뷰에서 변신 방법 후보를 추론한 뒤, 멀티모달 LLM이 실제 화면을 이해하고 조작을 수행하며 변신 여부를 확인합니다.

원문: https://www.ndss-symposium.org/ndss-paper/chameleoscan-demystifying-and-detecting-ios-chameleon-apps-via-llm-powered-ui-exploration/

### Contribution
- 개발자와 사용자가 공모하는 카멜레온 앱의 변신 방식과 유포 경로를 처음으로 체계적으로 정리했습니다.
- 정적 분석 기반 기존 도구(Chameleon-Hunter)가 놓치는 동적 렌더링 UI 기반 앱까지, 실제 실행과 UI 탐색으로 확인한다는 점이 차별점입니다.
- 방해 요소(광고, 팝업) 처리와 화면 요소 인식을 LLM에 맡겨 사람에 가까운 수준의 UI 탐색을 자동화했습니다.

### Evaluation
- 카멜레온 앱 131개와 정상 앱 233개로 만든 정답 데이터에서 정밀도 100%, 재현율 71.76%를 기록했습니다. 변신 관련 리뷰가 있는 앱으로 한정하면 재현율은 96.91%입니다.
- 변신 유형별로는 자동 변신형 95%, 시공간 조건형 100% 재현율을 보였지만, 입력 기반처럼 메타데이터 단서가 적은 유형은 상대적으로 낮습니다.
- 기반 LLM으로 GPT-4o를 썼고, 시스템은 모델에 독립적이라고 주장하지만 다른 모델로 교체한 결과는 제시하지 않았습니다. 정답 데이터 규모가 작아 정밀도 100%는 일반화에 주의가 필요합니다.

#### Comment
- 탐지 성능이 사용자 리뷰 같은 외부 단서에 크게 의존하므로, 리뷰가 없는 신규 앱에서는 효과가 떨어질 가능성이 큽니다.
- 모바일 앱 심사와 위장 앱 탐지에 LLM 기반 동적 UI 탐색을 적용한 실용적 사례입니다.
- 중국 기관 검증: 저장대학교 주도이며 올드도미니언대, 콜로라도광업대 연구자가 참여한 공동 연구입니다. 코드가 GitHub에 공개돼 있고, 재현율이 유형별로 차이가 나는 등 결과를 있는 그대로 보고하고 있어 포함했습니다.

---

**세부 분류: 온디바이스 LLM**

# PhishLang: A Real-Time, Fully Client-Side Phishing Detection Framework Using MobileBERT
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

경량 언어 모델 MobileBERT를 써서 피싱 사이트를 사용자 기기 안에서 실시간으로 탐지하는 크로미움 확장 프로그램 PhishLang을 제안합니다. 휴리스틱이나 정적 특징 기반 모델은 회피형 피싱에 약하고, 큰 딥러닝 모델은 클라이언트에서 돌리기 어렵다는 문제를 겨냥해 페이지 소스 코드의 맥락 구조를 직접 학습시켰습니다. 비슷한 구조 대비 메모리를 최대 7배 적게 쓰면서 최신 모델과 비슷한 탐지 성능을 냈고, 3.5개월 동안 실시간 운영해 블랙리스트가 놓친 피싱 URL 약 2만 6천 개를 찾았습니다.

원문: https://www.ndss-symposium.org/ndss-paper/phishlang-a-real-time-fully-client-side-phishing-detection-framework-using-mobilebert/

### Contribution
- 서버 조회 없이 기기 안에서 완결되는 언어 모델 기반 피싱 탐지를 처음 실용 수준으로 구현했고, 프레임워크와 확장 프로그램을 모두 공개했습니다.
- JS 회피, 클릭재킹, DOM 조작, 텍스트 인코딩 같은 16가지 현실적인 문제 공간 회피 공격에 대해 파서 수준 방어와 적대적 재학습을 결합해 강건성을 높였습니다.
- 탐지 결과를 블랙리스트 운영자에게 즉시 신고해, Google Safe Browsing의 JS 회피 공격 탐지율이 35%에서 73%로 오르는 등 실제 생태계 개선 효과를 보였습니다.

### Evaluation
- Certstream으로 2023년 9월부터 2024년 1월까지 4,270만 도메인을 검사해 25,796개를 피싱으로 판정했습니다. 무작위 2,500개를 두 명이 수작업 검증해 정밀도 95.5%(평가자 일치도 Cohen's Kappa 0.82)를 확인했습니다.
- 제로데이 상황에서 91% 이상을 탐지해 여러 기존 도구를 앞섰다고 보고합니다.
- 놓친 사례는 VirusTotal로 찾은 261개를 분석했는데, CAPTCHA와 QR 코드 같은 회피 기법이 주원인이었습니다. 재현율은 전체 모집단이 아니라 VirusTotal 기준으로만 측정됐다는 한계가 있습니다.

#### Comment
- 엄밀히는 브라우저 확장이지만, 클라이언트 측 경량 언어 모델로 보안 판단을 하는 구조라 모바일 기기 내 탐지 엔진 설계에 그대로 참고할 수 있어 온디바이스 분류에 넣었습니다.
- 텍사스대 알링턴 연구진의 논문이며 NDSS 게재 논문입니다.

---

**세부 분류: 프라이버시**

# ANONYCALL: Enabling Native Private Calling in Mobile Networks
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

통신사는 전화번호나 SUPI 같은 영구 식별자로 가입자를 관리하기 때문에 위치와 통화 이력을 추적할 수 있습니다. 영구 식별자 없이 망에 접속하는 익명 인증 기법은 이미 여럿 나와 있지만, 그렇게 접속한 단말에게 어떻게 전화를 걸고 사용량을 과금할지는 풀리지 않은 문제였습니다. ANONYCALL은 이 두 기능을 익명성을 깨지 않고 제공하는 통화 관리 구조입니다. 발신자는 수신자 쪽 인증 에이전트를 통한 대역 외 인증을 거쳐 수신자의 임시 SIP URI를 받아 VoLTE와 VoNR 같은 기본 통화 기능으로 바로 전화를 걸고, 과금은 이중 사용을 막는 익명 잔액 자격증명과 영지식 증명으로 처리합니다.

원문: https://www.ndss-symposium.org/ndss-paper/anonycall-enabling-native-private-calling-in-mobile-networks/

### Contribution
- 기존 익명 망 접속 연구가 비워 둔 수신자 탐색과 사용량 기반 과금을 함께 해결해, 익명 접속을 실제 통신 서비스로 쓸 수 있는 수준까지 끌어올렸습니다.
- 통화 경로에서 통신사는 임시 SIP URI와 망 내부 IP만 보게 되어 세션 간 연결이 불가능하고, 과금 쪽은 SPS-EQ 서명 기반 자격증명과 범위 증명으로 사용량을 증명하면서도 단말을 추적할 수 없게 설계했습니다.
- 기존 IMS 구조와 SIP 메시지를 바꾸지 않으므로 표준 프로토콜 수정 없이 배치할 수 있다는 점이 실용적인 장점입니다.

### Evaluation
- open5gs 기반 코어와 IMS, Android 프로토타입 앱, AWS에 둔 인증 에이전트로 실제 단말 두 대 사이의 통화를 시연했습니다. 임시 SIP URI 조회는 Wi-Fi 환경에서 약 80ms, 인증 포함 전체 과정은 50~180ms로 측정됐고 통화 수립 지연 증가는 200ms 미만이라고 보고합니다.
- 과금 프로토콜은 bn254 곡선 위에서 Cryptimeleon과 mcl 라이브러리로 단말과 서버 측 연산 시간을 측정했습니다.
- 지연 수치는 네트워크 조건에 크게 좌우되는 소규모 프로토타입 측정이라 상용망 규모의 부하나 다수 사용자 환경은 검증되지 않았습니다. 안전성은 실험이 아니라 형식적 증명 개요로 뒷받침됩니다.

#### Comment
- 익명 접속 계열(USENIX Security 2021, NDSS 2024, CCS 2024, S&P 2025)의 후속으로, 전제 조건인 익명 접속 기법 자체가 상용망에 도입되지 않은 상태라는 점이 가장 큰 한계입니다.
- 통신사가 이 구조를 채택할 유인이 무엇인지는 논문도 과금 지원 정도로만 다루고 있어, 기술적 가능성 연구로 보는 것이 맞습니다.
- 버지니아공대, 켄터키대, 조지아공대 공동 연구이며 NDSS는 보안 분야 최상위 학회입니다. 프로토타입 코드가 Zenodo에 공개돼 있습니다.

---

# Connecting the Dots: An Investigative Study on Linking Private User Data Across Messaging Apps
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

한 사람이 카카오톡, 텔레그램, 왓츠앱, 시그널, 틴더를 함께 쓰는 환경에서, 각 앱의 연락처 탐색, SSO 기반 계정 연동, 주변 사용자 검색 기능이 서로 맞물리면 어떤 프라이버시 위협이 생기는지 분석한 연구입니다. 저자들은 앱별로 개인 정보가 드러나는 경로를 확인한 뒤 이를 연결해, 한 플랫폼에서 익명으로 활동하는 사용자의 실명을 다른 플랫폼에서 찾아내고 위치까지 추정하는 교차 플랫폼 연결 공격을 처음으로 보였습니다. 전화번호와 프로필 사진이 플랫폼 사이를 잇는 열쇠 역할을 한다는 점이 핵심 결론입니다.

원문: https://www.ndss-symposium.org/ndss-paper/connecting-the-dots-an-investigative-study-on-linking-private-user-data-across-messaging-apps/

### Contribution
- 개별 앱 단위로만 연구되던 메시징 앱 프라이버시 문제를, 여러 앱을 동시에 쓰는 현실 환경에서 정보가 결합될 때의 위험으로 확장했습니다.
- 카카오톡의 연락처 등록 허용량이 지나치게 관대해 전화번호 소유자를 대규모로 식별할 수 있다는 점, 인기 웹사이트 63곳이 카카오 SSO 토큰을 URL이나 브라우저 저장소에 노출한다는 점을 실측으로 보였습니다.
- 연락처 탐색 정책을 강화해야 한다는 결론과 함께 플랫폼별 완화 방안을 제시했습니다.

### Evaluation
- 전화번호 하나로 운영하는 계정만으로 카카오톡 사용자 10만 5천여 명의 프로필을 수집할 수 있었고 성공률은 67.9%였습니다.
- 텔레그램과 카카오톡을 교차하면 무작위 번호 1,000개 중 텔레그램에 등록된 88명 가운데 70명(79.55%)의 실명 프로필을 확인했습니다.
- 틴더 위치 추정은 12번의 질의로 평균 오차 385m, 40번으로 324m를 달성해, 비슷한 정확도에 676번이 필요했던 기존 기법보다 훨씬 효율적입니다. 다만 위치 실험 표본은 무작위 10곳으로 작습니다.

#### Comment
- 한국 메시징 환경, 특히 인구 94%가 쓰는 카카오톡을 정면으로 다룬 드문 연구라 국내 서비스 사업자와 보안 담당자에게 직접적인 시사점이 있습니다. 서론에서도 익명 채팅방 사용자의 전화번호가 보이스피싱에 악용된 사례를 동기로 듭니다.
- 공격 결과는 측정 시점의 플랫폼 정책에 의존하므로, 공개 이후 정책이 바뀌었을 수 있습니다.
- KAIST와 메릴랜드대 공동 연구이며 NDSS 게재 논문입니다.

---

# Cross-Boundary Mobile Tracking: Exploring Java-to-JavaScript Information Diffusion in WebViews
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

Android WebView는 브라우저처럼 격리된 맥락에서 웹 콘텐츠를 실행하지만, 앱은 런타임에 자바스크립트를 주입하거나 Java 메서드를 자바스크립트에 노출해 이 경계를 넘나들 수 있습니다. 기존 분석 도구는 앱의 Java 코드만 보거나 WebView 안의 자바스크립트를 제대로 보지 못했습니다. 이 논문은 WebView 내부 자바스크립트 실행 추적과 Java 메서드 호출 정보를 결합한 동적 분석 도구 WebViewTracer를 만들고, Android 앱 1만 개를 분석했습니다. WebView를 쓰는 앱 4,597개 중 69% 이상이 광고 ID나 빌드 ID처럼 원래 자바스크립트가 접근할 수 없는 정보를 WebView에 주입했고, 그중 90%가 웹 API로 이를 제3자 서버에 보냈습니다.

원문: https://www.ndss-symposium.org/ndss-paper/cross-boundary-mobile-tracking-exploring-java-to-javascript-information-diffusion-in-webviews/

### Contribution
- VisibleV8 기반 자바스크립트 추적과 Frida 기반 Java 후킹을 묶어, Java에서 자바스크립트로 정보가 흘러가는 과정을 끝까지 따라가는 공개 도구를 만들었습니다.
- Java와 자바스크립트 경계를 넘는 정보 확산을 대규모로 처음 측정해, WebView 격리 모델이 광고와 추적 목적으로 사실상 무너지고 있음을 보였습니다.
- 주입의 출처를 스택 추적으로 가려 대부분이 앱 자체가 아니라 제3자 라이브러리에서 비롯된다는 점을 밝혔습니다.

### Evaluation
- 주입 중 96%가 앱에 포함된 제3자 라이브러리에서 발생했고, 1자 앱 코드에서 나온 것은 3.6%에 불과했습니다. WebView를 쓰는 앱의 53%가 빌드 ID를, 23.30%의 WebView가 광고 ID를 자바스크립트 맥락에 주입했습니다. 주요 출처는 Unity, ironSource 같은 광고 SDK였습니다.
- 자동 UI 탐색 도구가 수동 상호작용 대비 WebView의 약 50%만 도달했다고 스스로 밝히므로, 결과는 하한값으로 해석해야 합니다.
- 페이스북, 인스타그램 등 인기 앱 수동 분석에서 기존 연구가 보고하지 않은 주입 유형 7가지와 Java-자바스크립트 브리지 9개를 새로 찾았습니다.

#### Comment
- 앱 보안 SDK를 만드는 입장에서는 WebView 브리지(addJavascriptInterface, evaluateJavascript)가 기기 식별 정보 유출 경로가 된다는 점, 그리고 그 주체가 대부분 광고 SDK라는 점이 실무적으로 유용한 근거입니다.
- 노스캐롤라이나주립대, 크레타공대, 일리노이대 시카고 공동 연구로 도구가 GitHub에 공개돼 있습니다.

---

# Hey there! You are using WhatsApp: Enumerating Three Billion Accounts for Security and Privacy
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

메신저는 주소록의 전화번호로 가입 여부를 조회해 대화 상대를 찾게 해 주는데, 이 구조 자체가 전화번호 열거 공격을 가능하게 합니다. 이 논문은 왓츠앱의 속도 제한이 사실상 작동하지 않아 시간당 1억 개가 넘는 번호를 차단 없이 조회할 수 있음을 보이고, 이를 통해 35억 개 활성 계정 전체를 확인했습니다. 2021년 페이스북 유출 번호의 절반가량이 여전히 왓츠앱에서 활성 상태였고, 일부 X25519 공개키가 여러 기기와 번호에서 재사용되는 현상도 발견했습니다.

원문: https://www.ndss-symposium.org/ndss-paper/hey-there-you-are-using-whatsapp-enumerating-three-billion-accounts-for-security-and-privacy/

### Contribution
- 245개국의 번호 체계를 바탕으로 실제로 배정될 수 있는 휴대전화 번호 후보를 약 630억 개로 좁히는 방법을 만들었습니다.
- 종단간 암호화로 메시지가 보호되더라도 연락처 탐색 기능만으로 국가별 사용자 수, 증감, 운영체제 비율, 보조 기기 사용률 같은 거시 정보를 얻을 수 있음을 보였습니다.
- 서로 다른 계정에서 같은 공개키가 쓰이는 사례를 찾아, 비공식 클라이언트의 잘못된 구현이나 사기 활동 가능성을 제기했습니다.

### Evaluation
- 결과는 실제 측정입니다. 수집된 데이터는 개인 단위 분석을 하지 않고 집계 통계로만 다뤘다고 밝히며, 국가별 보조 기기 사용률(네덜란드, 이스라엘 22% 이상, 일부 국가 3% 미만), 월별 이탈률(벨기에 1% 미만, 인도 2%) 같은 수치를 제시합니다.
- Meta와의 공개 절차를 날짜별로 상세히 기록했고, Meta는 최종본에 공식 입장을 내고 완화 조치를 진행 중이라고 밝혔습니다.
- 측정 자체가 정확도를 따질 성격은 아니며, 수치의 신빙성은 측정 범위의 완전성에 달려 있습니다. 저자들은 데이터를 공개하지 않습니다.

#### Comment
- 전화번호 하나로 가입 여부, 프로필 사진, 상태 문구를 확인할 수 있다는 점은 스미싱과 보이스피싱 표적 선정에 직접 악용될 수 있어 모바일 사기 대응 관점에서 의미가 큽니다.
- 공개 전 수정이 이뤄지지 않은 상태에서 프리프린트를 냈다는 점이 논쟁적일 수 있으나, 저자들은 그 판단 근거를 투명하게 설명합니다.
- 빈대학교와 SBA Research 공동 연구이며 NDSS 게재 논문입니다.

---

# MVPNalyzer: An Investigative Framework for Auditing the Security & Privacy of Mobile VPNs
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

VPN 앱은 사용자 트래픽 전체를 가로채는 특권적 위치에 있어, 통신사에 대한 신뢰가 VPN 사업자로 옮겨 갈 뿐입니다. 그런데 모바일 VPN 앱은 충분히 감사받지 못하고 있습니다. 이 논문은 Android VPN 앱을 네트워크 계층별로 분석하는 확장형 프레임워크 MVPNalyzer를 만들고, Google Play의 인기 VPN 앱 281개를 조사했습니다. 61개가 암호화되지 않은 데이터를 보냈고(그중 5개는 VPN 설정 파일을 평문으로 보내 터널 탈취가 가능), 29개는 DNS를 포함한 트래픽을 터널 밖으로 흘렸으며, 76개는 광고 ID를 전송했습니다.

원문: https://www.ndss-symposium.org/ndss-paper/mvpnalyzer-an-investigative-framework-for-auditing-the-security-privacy-of-mobile-vpns/

### Contribution
- 실제 기기에서 VPN 앱을 자동으로 설치, 연결, 측정하고 터널 안팎의 트래픽을 비교하는 분석 파이프라인을 만들었습니다. Android VPN 인터페이스를 다른 용도로 쓰는 앱(백신, DNS 변경 앱)을 걸러 내는 기준도 정리했습니다.
- 평문 전송, 트래픽 누출, 차단 회피용 트래픽 위장 여부, 추적 식별자 전송, OpenVPN 설정의 보안 모범 사례 준수라는 다섯 축으로 결과를 체계화했습니다.
- 영향을 받는 앱들의 누적 설치 수가 수억 건에 이른다는 점을 보여 개발자 관리 소홀의 규모를 드러냈습니다.

### Evaluation
- 40개 검색어와 VPN 카테고리를 모든 국가에서 수집한 뒤, 계정이나 결제가 필요 없는 실제 작동 앱 281개를 Android 14 실기기에서 시험했습니다.
- 평문 흐름 10,552건, 143개 앱의 트래픽 위장 미적용, 107개 앱의 설정 파일 모범 사례 미준수, 80% 이상(246개)의 광고 및 추적 도메인 접속 등을 정량적으로 보고합니다.
- 트래픽 누출 판정에 방문 도메인 90% 이상이 터널 밖에서 보이면 누출로 보는 임계값을 쓰는 등 판단 기준이 명시돼 있어 재현과 비교가 쉽습니다. 유료 및 계정 필요 앱은 빠졌으므로 시장 전체를 대표하지는 않습니다.

#### Comment
- 보안 앱을 표방하는 VPN이 오히려 식별자 수집과 평문 전송 통로가 될 수 있다는 점은 모바일 보안 제품 평가 기준을 세울 때 참고할 만합니다.
- 미시간대(로야 엔사피 연구실, 검열과 VPN 측정 분야 대표 연구실)와 뉴멕시코대 공동 연구이며 NDSS 게재 논문입니다.

---

# Passive Multi-Target GUTI Identification via Visual-RF Correlation in LTE Networks
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

LTE는 영구 식별자 IMSI 노출을 막으려고 임시 식별자 GUTI를 씁니다. 이 논문은 카메라로 관찰한 기기 사용 시점과 상용 SDR로 수신한 제어 평면 메시지의 시점을 맞춰 보는 것만으로, 신호를 전혀 송신하지 않고도 시야 안 여러 기기의 GUTI를 동시에 식별할 수 있음을 보입니다. 사용자 조작을 세 번 정도 관찰하면 식별이 가능했고, 일부 상용망에서는 GUTI가 최대 33일 동안 바뀌지 않았으며 재할당도 연결 가능한 경우가 많았습니다. 한번 연결된 GUTI는 페이징과 RRC 메시지 수신만으로 셀 또는 페이징 영역 단위의 위치 추적에 쓰일 수 있습니다.

원문: https://www.ndss-symposium.org/ndss-paper/passive-multi-target-guti-identification-via-visual-rf-correlation-in-lte-networks/

### Contribution
- 전화번호 같은 사전 정보와 능동적 페이징 유도가 필요했던 기존 GUTI 공격과 달리, 수신만 하는 수동 방식으로 여러 대상을 병렬 식별하는 새 위협 모델을 정식화했습니다.
- 제어 메시지 일부가 누락돼도 복구되는 유한 상태 기계 기반 식별 알고리즘을 제안했습니다.
- 상용망의 GUTI 수명과 재할당 패턴을 실측해 표준 권고와 실제 운영 사이의 차이를 수치로 보였습니다. GSMA에 책임 있는 공개를 했습니다.

### Evaluation
- 두 나라 네 개 통신사에서 12회 실험, 단말별 37회 시도 중 36회(97%) 추출, 35회(94%) 완전 검증에 성공했습니다. 아이폰과 퀄컴, 엑시노스 칩셋 삼성 단말을 섞어 칩셋 의존성이 없음을 확인했습니다.
- 제어 패킷 손실이 약 16%인 열악한 환경에서도 동작했고, 스니퍼 처리율은 73~100%였습니다.
- 대상 단말 수와 실험 장소가 제한적이고 대상 기기를 의도적으로 카메라 시야에 배치한 통제된 실험이므로, 혼잡한 공공장소에서의 성공률은 별도 검증이 필요합니다.

#### Comment
- CCTV가 이미 깔린 환경에서는 짧은 영상 관찰을 장기 무선 추적으로 바꿀 수 있다는 점에서, GUTI 재할당 주기 같은 통신사 운영 정책의 중요성을 보여 줍니다.
- 국가보안기술연구소(ETRI 부설) 연구진의 논문으로, 국내 연구기관의 이동통신 보안 연구가 NDSS에 실린 사례입니다.

---

# PriSrv+: Privacy and Usability-Enhanced Wireless Service Discovery with Fast and Expressive Matchmaking Encryption
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

Wi-Fi, BLE, mDNS 같은 무선 서비스 탐색 프로토콜은 광고를 평문으로 내보내 기기 추적과 세션 연결, 사칭 공격에 노출됩니다. PriSrv+는 NDSS 2024의 PriSrv를 개선한 프라이버시 보호 서비스 탐색 프로토콜로, 핵심은 새 매치메이킹 암호 FEME입니다. FEME는 임의 문자열을 속성으로 쓸 수 있는 표현력 있는 접근 정책을 지원하면서 메시지와 속성 값을 숨깁니다. PriSrv 대비 암호화 7.62배, 복호화 6.23배 빨라졌고 암호문 크기는 87.33% 줄었습니다.

원문: https://www.ndss-symposium.org/ndss-paper/prisrv-privacy-and-usability-enhanced-wireless-service-discovery-with-fast-and-expressive-matchmaking-encryption/

### Contribution
- 무한 속성 공간을 지원하는 최초의 매치메이킹 암호 FEME를 설계해, 고정된 이진 벡터 속성만 쓰던 PriSrv의 제약을 없앴습니다.
- 속성 이름만 드러내고 값은 숨기는 방식으로 복호화 없이 빠른 필터링을 유지하면서 추적 위험을 제거했습니다.
- mDNS, BLE, Wi-Fi와 호환되도록 설계했고, 서비스 광고와 익명 상호 인증 단계의 통신량을 각각 87.33%, 86.64% 줄였습니다. 형식적 안전성 증명을 제공합니다.

### Evaluation
- 데스크톱에서 세 가지 곡선(MNT159, MNT201, BN256)에 대해 기존 ACME와 같은 속성 수와 정책 조건으로 연산 및 통신 비용을 비교했고, 여러 플랫폼에서 프로토콜 전체 성능도 측정했습니다.
- 비교 조건을 동일하게 맞춘 점은 공정하지만, 보안 수준 80~100비트의 곡선을 사용해 현재 권장되는 128비트 수준과는 차이가 있습니다.
- 실제 대규모 무선 환경 배치 실험은 없고 마이크로벤치마크 중심의 평가입니다.

#### Comment
- 암호 프로토콜 설계 논문이라 실무 적용보다는 무선 기기 탐색의 프라이버시 설계 방향을 참고하는 용도에 적합합니다.
- 싱가포르경영대학교 주도이며 오리건대, 하이난대, 지난대가 참여했습니다. 중국 기관 검증: 중국 측 공저자 웡젠(지난대)은 응용 암호 분야에서 오래 활동한 실재 연구자이고, 주 저자 소속인 싱가포르경영대 로버트 덩 교수 연구실도 저명합니다. 코드가 Zenodo와 GitHub에 공개돼 있고 형식 증명을 갖춰 포함했습니다.

---

**세부 분류: TEE 및 사이드 채널**

# Side-channel Inference of User Activities in AR/VR Using GPU Profiling
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

AR/VR 기기에서 악성 앱이 다른 앱을 감시하는 공격은 대개 고해상도 성능 카운터와 앱 동시 실행을 전제로 했지만, Meta Quest처럼 독립 앱 동시 실행이 막힌 기기에서는 통하지 않습니다. 이 논문의 OVRWATCHER는 기기에 내장된 GPU 프로파일러로 1Hz의 낮은 해상도 GPU 지표만 백그라운드에서 수집해 사용자 활동을 추론하는 부채널입니다. 추가 SDK 설치나 앱 데이터 접근 없이, 어떤 앱을 쓰는지는 물론 쇼핑 앱에서 고른 상품이나 가상 회의 참가자 수까지 알아낼 수 있었습니다.

원문: https://www.ndss-symposium.org/ndss-paper/side-channel-inference-of-user-activities-in-ar-vr-using-gpu-profiling/

### Contribution
- 동시 실행 없이도 동작하는 저해상도 GPU 부채널을 AR/VR 기기에서 처음 보였습니다.
- 72개 GPU 지표 중 텍스처 밉맵 관련 지표가 화면 속 3D 객체의 크기, 거리, 이동 속도와 강하게 상관한다는 점을 체계적으로 분석했습니다. 픽셀 수와의 상관계수가 VR 모드에서 0.94~0.99였습니다.
- Meta 버그 바운티를 통해 공개했고 Meta로부터 포상을 받았습니다.

### Evaluation
- Meta Quest 앱스토어 인기 무료 앱 100개 지문 식별에서 랜덤 포레스트 기준 99.5% 정확도를 냈고, 지표 하나만 써도 F1 90% 이상이었습니다. 객체 단위 추론은 98% 이상입니다.
- 실제 참가자가 고른 가상 객체를 주변 환경 잡음 속에서도 최대 88% 정확도로 구분했고, 지표가 제한된 기기 간 설정에서도 모든 사례 연구에서 93% 이상을 유지했습니다.
- 앱마다 20회씩 측정한 통제된 데이터셋이라 실사용 환경의 다양성은 일부만 반영됐습니다.

#### Comment
- 모바일 기기와 같은 계열의 SoC를 쓰는 XR 기기에서 GPU 프로파일링 API 접근 통제가 부채널 방어의 핵심이 된다는 점을 보여 줍니다.
- 아이오와주립대, 퍼듀대, 샤르자아메리칸대 공동 연구이며 NDSS 게재 논문입니다.

---

# XR Devices Send WiFi Packets When They Should Not: Cross-Building Keylogging Attacks via Non-Cooperative Wireless Sensing
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

기존 XR 키 입력 추론 공격은 시야 확보나 10m 이내 근접을 전제로 했습니다. 이 논문은 Wi-Fi 무선 센싱을 이용해 시야 없이도, 건물을 사이에 두고 최대 30m 거리에서 동작하는 키로깅 공격을 제안합니다. 핵심은 Wi-Fi 칩셋의 취약점으로, 공격자가 위조한 암호화되지 않은 패킷을 보내면 피해자 기기가 자동으로 ACK 패킷을 되돌려 줍니다. 이를 반복해 헤드셋이 계속 패킷을 보내게 만들고, 수집한 채널 상태 정보(CSI)로 손과 손가락 위치를 추정해 입력을 알아냅니다. 전용 송신기나 가짜 핫스팟이 필요 없다는 점이 기존 Wi-Fi 기반 공격과 다릅니다.

원문: https://www.ndss-symposium.org/ndss-paper/xr-devices-send-wifi-packets-when-they-should-not-cross-building-keylogging-attacks-via-non-cooperative-wireless-sensing/

### Contribution
- 시야 없이 장거리에서 동작하는 최초의 XR 키로깅 공격을 제안했습니다.
- 헤드셋 자체를 송신기로 바꿔, 네트워크 접근 없이도 CSI를 대량 수집할 수 있음을 보였습니다. 피해자가 공격자의 송신기와 수신기 사이에 있어야 한다는 제약을 없앴습니다.
- 학습 데이터 없이 사용자 동작을 추정하는 비지도 무선 센싱 기법을 제시하고 구현과 데이터를 공개하겠다고 밝혔습니다.

### Evaluation
- Meta Quest 2와 3을 대상으로 1~30m 거리, -90°~+90° 각도, 벽 너머, 여러 사용자 조건에서 평가했습니다. 15자 길이 비밀번호에 대해 건물 간 설정에서 상위 25개 후보 기준 78.6% 정확도를 보고합니다.
- 건물 간 30m 실험에서는 상위 1개 16.30%, 상위 4개 51.40%, 상위 9개 74.30%로, 거리가 멀수록 상위 1개 정확도는 크게 떨어집니다.
- 처음 보는 사용자와 헤드셋에서도 비슷한 성능을 보여 일반화 가능성을 뒷받침하지만, 상위 1개 정확도가 낮아 실제 단독 입력 복원보다는 후보 좁히기에 가깝습니다.

#### Comment
- 모바일 및 XR 기기의 Wi-Fi 칩셋이 암호화되지 않은 패킷에 자동 응답한다는 하위 계층 특성이 물리적 부채널로 이어진다는 점에서, 기기 하드닝 관점의 시사점이 있습니다.
- UCLA 연구진의 논문이며 NDSS 게재 논문입니다.

---

**세부 분류: 그 외**

# AirSnitch: Demystifying and Breaking Client Isolation in Wi-Fi Networks
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

클라이언트 격리는 같은 Wi-Fi 망의 단말끼리 직접 통신하지 못하게 막아 ARP 스푸핑 같은 내부자 공격을 차단하는 기능입니다. 그러나 표준화돼 있지 않아 구현마다 정책이 제각각이고 보안 보장이 불분명합니다. 이 논문은 Wi-Fi 암호화, 패킷 스위칭, 라우팅 세 계층에서 클라이언트 격리를 구조적으로 분석해 이를 우회하는 새로운 공격들을 찾았습니다. 브로드캐스트 프레임 키의 잘못된 관리, MAC 또는 IP 한쪽에서만 이뤄지는 격리, 네트워크 스택 전반의 약한 신원 동기화가 근본 원인이며, 시험한 모든 라우터와 망이 최소 하나의 공격에 취약했습니다.

원문: https://www.ndss-symposium.org/ndss-paper/airsnitch-demystifying-and-breaking-client-isolation-in-wi-fi-networks/

### Contribution
- 클라이언트 격리를 우회해 상향과 하향 트래픽 모두에 대한 완전한 중간자 공격을 가능하게 하는 새로운 공격 요소를 제시했습니다.
- 단일 BSSID 가정용 망에서는 모든 WPA 버전에서 클라이언트 격리가 근본적으로 무력화된다는 점을 보였습니다.
- 유선으로 연결된 내부 기기의 트래픽까지 가로채 백엔드 RADIUS 약한 비밀번호를 깨는 등 상위 계층 공격으로 확장했고, 코드를 공개했습니다.

### Evaluation
- 인기 제조사 가정용 라우터 5종과 오픈소스 배포판 DD-WRT, OpenWRT, 그리고 실제 대학 네트워크 두 곳에서 공격을 검증했습니다.
- 가상 BSSID 사이의 격리가 많은 기기에서 누락되거나 잘못 설정돼 있음을 확인했고, 권장 설정을 적용한 DD-WRT와 OpenWRT는 포트 스틸링을 막았습니다.
- 다양한 제조사와 실제 망을 포함해 일반화 근거가 탄탄하며, 아티팩트가 Zenodo와 GitHub에 공개돼 재현 가능합니다.

#### Comment
- 가정과 기업 Wi-Fi에서 흔히 안전하다고 여기는 클라이언트 격리가 사실상 신뢰하기 어렵다는 점을 보여, 모바일 기기가 접속하는 무선망의 신뢰 모델을 재검토하게 합니다.
- UC 리버사이드와 KU 뢰번(Mathy Vanhoef, Wi-Fi 보안 분야 대표 연구자) 공동 연구이며 NDSS 게재 논문입니다.

---

# BLERP: BLE Re-Pairing Attacks and Defenses
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

BLE 보안은 장기 키를 만드는 페어링과 세션 키로 통신을 암호화하는 세션 수립에 기댑니다. 표준은 이미 페어링된 기기가 보안 수준을 새로 협상하려고 다시 페어링하는 것을 허용하는데, 이 재페어링의 보안 함의는 그동안 검토되지 않았습니다. 이 논문은 Bluetooth Core Specification v6.1의 재페어링을 분석해 설계 취약점 6개(새로운 것 4개 포함, 예: 인증되지 않은 재페어링, 보안 수준 다운그레이드)를 찾고, 이를 악용하는 네 가지 공격 BLERP를 제시합니다. 사용자 조작이 거의 또는 전혀 없이 기기 사칭과 중간자 공격이 가능합니다.

원문: https://www.ndss-symposium.org/ndss-paper/blerp-ble-re-pairing-attacks-and-defenses/

### Contribution
- BLE 재페어링을 처음으로 보안 분석해, Bluetooth 버전이나 보안 수준과 무관하게 표준을 따르는 모든 기기에 영향을 주는 설계 결함을 밝혔습니다.
- 저가 하드웨어(nRF52)와 오픈소스로 재현 가능한 공격 및 중간자 시험 도구를 공개했습니다.
- 즉시 배포 가능한 재페어링 하드닝과, 설계 수준에서 문제를 해결하는 인증 재페어링 프로토콜 두 가지 방어책을 제시하고 ProVerif로 형식 검증했습니다.

### Evaluation
- BLE 호스트 15종, 컨트롤러 12종을 포함한 22개 대상에서 공격을 검증했습니다. Bluetooth 4.2~5.4와 가장 안전한 설정(SC, SCO, 인증 페어링)에서도 영향이 확인됐습니다.
- Apple, Android, NimBLE 스택에서 구현 결함도 추가로 발견했습니다. I/O가 없는 기기에는 0-click, I/O가 있는 기기에는 1-click으로 동작합니다.
- 최신 Bluetooth 버전 기기는 시장에 없어 시험하지 못했다는 한계를 명시합니다.

#### Comment
- Bluetooth SIG는 문제를 인정했으나 표준을 바꾸지 않을 계획이라고 밝혔고, Apple(iOS/macOS 26), Google(Android 16), Apache는 완화 조치를 취했습니다. 표준 결함인 만큼 개별 벤더 패치만으로는 완전히 해소되지 않습니다.
- 유럽 EURECOM 연구진(Daniele Antonioli, Bluetooth 보안 분야 대표 연구자)의 논문이며 NDSS 게재 논문입니다.

---

# BSFuzzer: Context-Aware Semantic Fuzzing for BLE Logic Flaw Detection
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

BLE는 설계가 복잡해 잘못 해석된 필드나 잘못된 상태 전이 같은 미묘한 논리 결함이 생기고, 이는 인증 우회나 서비스 거부로 이어질 수 있습니다. 이런 결함은 기존 퍼징이나 형식 분석으로는 잘 드러나지 않습니다. BSFuzzer는 Bluetooth Core Specification을 LLM 에이전트로 파싱해 상태 기계와 패킷 의미를 추출하고, 필드 수준과 상태 수준의 변이를 만들어 실제 기기에 시험하는 블랙박스 의미 기반 퍼징 프레임워크입니다. 응답이 기대 동작과 맞는지도 LLM이 검증해 전통 퍼저가 놓치는 논리 결함을 찾습니다.

원문: https://www.ndss-symposium.org/ndss-paper/bsfuzzer-context-aware-semantic-fuzzing-for-ble-logic-flaw-detection/

### Contribution
- LLM을 의미 추론 엔진으로 써서 프로토콜 의도를 해석하고 맥락 기반 변이를 유도하는 BLE 퍼징 프레임워크를 제안했습니다.
- 사양이 정한 의미 제약을 필드 및 상태 변이에 반영해, 의존성이 일관된 상태 인식 테스트 케이스를 생성합니다.
- 실제 기기 19대에서 34개의 미공개 버그를 찾아 9개가 CVE를 받았고, 주요 벤더 버그 바운티로 두 건이 인정됐습니다.

### Evaluation
- SoC 모듈 9종과 스마트폰 10종에서 총 36개 보안 문제를 찾았습니다. 기존 최고 커버리지 도구 Proteus 대비 코드 커버리지가 9.34% 높았습니다.
- LLM의 사양 분석 정확도는 최대 97%(패킷 의존성), 응답 검증 정확도는 최대 85.8%로 보고합니다. 22개 LL과 10개 SMP 메시지 순서도가 모두 올바르게 상태 기계로 변환됐습니다.
- LLM 응답 검증 정확도가 85% 수준이라 자동 판정에 일부 오탐과 미탐이 남으며, 최종 버그는 수작업 확인이 필요합니다.

#### Comment
- 사양 문서를 LLM으로 해석해 프로토콜 퍼징에 쓰는 접근은, 복잡한 모바일 무선 프로토콜 구현 검증에 적용할 수 있는 실용적 방향입니다.
- 중국 기관 검증: 시디안대, 하이난대, 중국과학원대, 칭화대 등 다수 중국 기관과 일본 가나자와대, 미국 노던애리조나대가 참여한 공동 연구입니다. 34개 버그 중 9개가 CVE로, 두 건이 벤더 바운티로 외부 인정을 받았고 코드가 GitHub에 공개돼 재현성이 확인되므로 포함했습니다. 교신저자 장위칭(중국과학원대), 리치(칭화대)는 보안 분야에서 실적이 확인되는 연구자입니다.

---

# Better Safe than Sorry: Uncovering the Insecure Resource Management in App-in-App Cloud Services
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

위챗, 틱톡, 알리페이, 바이두 같은 슈퍼앱은 미니앱 개발자에게 클라우드 데이터베이스, 스토리지, 클라우드 함수를 제공하고 사용자 식별자도 넘겨줍니다. 그런데 사용자가 자기 자원에만 접근하는지 검사하는 일은 미니앱 개발자 몫이라, 이 검사를 빠뜨리거나 잘못 구현하면 다른 사용자의 데이터를 읽거나 결제를 우회할 수 있습니다. 이 논문은 이를 처음으로 체계적으로 조사하고, 정적 분석과 동적 탐침을 결합한 ICREMINER로 실제 미니앱의 취약점을 찾아냈습니다. 클라우드 API를 쓰는 미니앱 22,695개 중 2,815개(12.40%), 8,062개 클라우드 연산에서 문제가 확인됐습니다.

원문: https://www.ndss-symposium.org/ndss-paper/better-safe-than-sorry-uncovering-the-insecure-resource-management-in-app-in-app-cloud-services/

### Contribution
- 슈퍼앱이 제공하는 신원 관리 구조에서 책임이 미니앱 개발자에게 넘어가는 지점을 문서 분석으로 정리하고, 이를 새로운 취약점 유형으로 정의했습니다.
- 클라이언트 쪽 클라우드 연산을 정적으로 추출하고, 데이터베이스 이름이나 파일 ID 같은 접근 대상을 추론한 뒤 실제로 접근 가능한지 동적으로 확인하는 자동화 도구를 만들었습니다.
- 대형 기업의 미니앱도 영향을 받는다는 점을 보이고 책임 있는 공개와 완화 방안을 함께 제시했습니다.

### Evaluation
- 네 플랫폼의 미니앱 약 125만 개에서 클라우드 API를 쓰는 22,695개를 추렸습니다. 미니앱 하나를 분석하는 데 평균 약 77초가 걸렸습니다.
- 도구가 탐지한 3,057개 앱, 8,289개 연산을 전문가 세 명이 합의 방식으로 수작업 검증했고, 그중 97.26%가 실제로 민감한 자원을 노출하는 것으로 확인됐습니다. 읽기 연산이 있는 1,943개 앱은 테스트 계정 두 개로 실제 무단 접근을 시연했습니다.
- 쓰기 연산은 윤리적 이유로 실제 실행하지 않고 코드 의미 분석으로 영향을 추정했기 때문에, 결제 우회 같은 피해 규모는 추정치에 가깝습니다. 탐지하지 못한 취약점(재현율)은 측정되지 않았습니다.

#### Comment
- 국내에서도 카카오톡, 토스처럼 미니앱 생태계를 키우는 흐름이 있어, 플랫폼이 인증은 제공하되 인가는 개발자에게 맡기는 구조의 위험을 보여 주는 사례로 참고할 만합니다.
- 대부분의 취약 앱이 위챗(2,057개)에 몰려 있어 결과가 특정 플랫폼 생태계에 크게 의존합니다.
- 중국 기관 검증: 푸단대학교 시스템 보안 연구실(양민, 양즈민 교수)은 모바일과 미니앱 보안 분야에서 최상위 학회 실적이 꾸준한 실재 연구실입니다. 수작업 검증 절차와 윤리적 고려가 구체적으로 서술돼 있고 아티팩트가 Zenodo에 공개돼 있으며, 수치가 비정상적으로 좋은 구조도 아니라서 포함했습니다.

---

# Formal Analysis of BLE Secure Connection Pairing and Revelation of the PE Confusion Attack
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

BLE Secure Connection(SC) 페어링은 BLE 채널로 오가는 민감 정보를 보호하는 최신 보안 프로토콜입니다. 그러나 흐름이 복잡하고 페어링 방식 선택을 형식화하기 어려우며 사용자 가정이 지나치게 이상적이라, 그동안 엄밀한 형식 분석이 부족했습니다. 이 논문은 Tamarin으로 BLE-SC 페어링을 참여자별 상태 기계와 페어링 방식 선택 논리까지 반영해 분석합니다. 임시 대역 외 채널 유출 같은 더 강한 공격자 능력을 가정해 84개 페어링 경우를 검증했고, 그 과정에서 새로운 중간자 공격인 PE confusion 공격을 찾았습니다.

원문: https://www.ndss-symposium.org/ndss-paper/formal-analysis-of-ble-secure-connection-pairing-and-revelation-of-the-pe-confusion-attack/

### Contribution
- 호스트와 컨트롤러를 분리된 개체로 모델링하고 페어링 방식 선택 논리까지 형식화한, 가장 상세한 BLE-SC 페어링 기호 모델을 제시했습니다.
- 기존의 method confusion 공격을 재현함과 동시에 새 PE confusion 공격을 발견하고, 통제된 환경에서 재현할 수 있는 도구와 개념 증명을 제공했습니다.
- 기기 능력과 보안 요구에 따른 84개 경우 각각에 대해 안전을 보장하는 최소 보안 가정을 제시하고 방어책을 제안했습니다.

### Evaluation
- Tamarin Prover로 모델을 검증했고, 시간과 연산 자원 제약으로 대표적인 16개 경우를 추려 분산 검증했습니다. 아티팩트가 Zenodo와 GitHub에 공개돼 재현 절차가 상세히 기술됩니다.
- 전체 84개 모델 중 16개만 실제 재현 실험으로 돌렸다는 점은 자원상의 선택이지만, 생성과 검증 과정이 동일하다는 근거로 축소를 정당화합니다.
- 형식 검증 기반이라 실제 상용 기기 공격 성공률 같은 실측은 PoC 수준으로만 제시됩니다.

#### Comment
- BLE 페어링의 안전이 사용자 행동과 기기 능력 조합에 따라 어떻게 달라지는지 형식적으로 정리해, 무선 페어링 보안 설계의 참고 자료로 유용합니다.
- 중국 기관 검증: 우한대 정보보안 연구실(천징 교수 교신)과 홍콩이공대 공동 연구입니다. 우한대 해당 연구실은 보안 분야 실적이 꾸준하고, 형식 모델과 PoC가 Zenodo 및 GitHub에 공개돼 검증 가능하며, Tamarin 기반 증명이라 성능 수치를 부풀릴 구조가 아니므로 포함했습니다.

---

# SIPConfusion: Exploiting SIP Semantic Ambiguities for Caller ID and SMS Spoofing
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

SIP는 VoIP, VoLTE, RCS 메시징의 신호 표준이며, 발신자 신원을 확인하는 인증과 신원 주장 메커니즘을 갖추고 있습니다. 그러나 표준이 유연한 만큼 서버와 단말이 같은 메시지를 서로 다르게 해석할 여지가 있고, 이 해석 차이가 신원 위조로 이어질 수 있습니다. 이 논문은 이런 의미 모호성 기반 위조 취약점을 체계적으로 찾는 블랙박스 퍼징 프레임워크 SIPCHIMERA를 제안하고, 오픈소스 SIP 서버 6종과 단말 9종 조합 대부분에서 발신번호와 SMS 위조가 가능함을 확인했습니다. 실제 VoIP 기기, 상용 SIP 서비스, 통신사급 RCS 플랫폼에서도 영향이 확인돼 제조사들에 공개했습니다.

원문: https://www.ndss-symposium.org/ndss-paper/sipconfusion-exploiting-sip-semantic-ambiguities-for-caller-id-and-sms-spoofing/

### Contribution
- 개별 구현의 버그가 아니라 서버와 단말 사이의 해석 불일치라는 관점에서 SIP 신원 위조를 처음 체계적으로 조사했습니다.
- RFC 문법에서 신원 관련 요소를 뽑아 시험 입력을 만들고, 단말에 실제로 표시되는 신원과 비교하는 자동화 방법을 설계했습니다.
- STIR/SHAKEN 같은 서명 기반 대책이 도입된 환경에서도 구현 간 해석 차이가 새로운 우회 경로가 된다는 점을 보이고 완화 방안을 제안했습니다.

### Evaluation
- Asterisk, OpenSIPS, Kamailio 등 서버 6종과 Zoiper, Linphone 등 단말 9종으로 시험 환경을 만들어, 인증된 공격자와 인증되지 않은 공격자 시나리오를 모두 평가했습니다. 서버는 각 공식 문서의 보안 권장 설정을 따랐습니다.
- 실제 환경 검증으로 VoIP 기기 5종, 상용 SIP 서비스 7곳, 통신사급 RCS 문자 플랫폼 3곳을 시험했습니다.
- 결과는 취약점 존재 여부를 확인하는 방식이며, 상용 통신망 전반에서 얼마나 악용 가능한지는 시험한 범위로 한정됩니다.

#### Comment
- 보이스피싱과 스미싱의 출발점인 발신자 위조가 프로토콜 해석 수준에서 여전히 가능하다는 점에서, 통화 기반 사기 탐지를 다루는 모바일 보안 연구에 중요한 배경 자료입니다.
- 중국 기관 검증: 칭화대 두안하이신, 천젠쥔 교수 연구실은 프로토콜 모호성과 웹 및 네트워크 보안 분야에서 최상위 학회 실적이 꾸준한 실재 연구실입니다. 시험 대상이 모두 공개 소프트웨어이고 도구가 GitHub에 공개돼 재현이 가능하며, 책임 있는 공개 이력도 명시돼 있어 포함했습니다.

---

# Small Cell, Big Risk: A Security Assessment of 4G LTE Femtocells in the Wild
> NDSS 2026 (Network and Distributed System Security Symposium), 2026년 2월 발표
> 2026

펨토셀은 통신사가 실내 커버리지를 넓히려고 가정이나 사무실에 두는 소형 기지국입니다. 일반 기지국과 달리 공격자가 하드웨어에 물리적으로 접근하기 쉬워 새로운 공격면이 됩니다. 이 논문은 상용 펨토셀 기기와 인터넷 전수 측정을 함께 활용해 4G LTE 펨토셀을 처음으로 체계적으로 평가했습니다. 상용 기기 4종의 소프트웨어와 하드웨어를 분석해 로컬 또는 원격 장악으로 이어지는 공통 취약점 5개를 찾았고, 인터넷에서 펨토셀로 의심되는 기기 86,108대를 식별했습니다. 하나만 장악해도 이동통신 코어망과 가입자 공격의 발판이 된다는 점을 실제 통신망에서 검증했습니다.

원문: https://www.ndss-symposium.org/ndss-paper/small-cell-big-risk-a-security-assessment-of-4g-lte-femtocells-in-the-wild/

### Contribution
- 상용 기기 분석과 인터넷 규모 측정을 결합해 4G 펨토셀의 보안을 처음으로 종합 평가했습니다.
- 장악한 펨토셀이 코어망과 가입자 모두에 대한 공격 거점이 될 수 있음을 실제 운영망 실험으로 입증했습니다.
- GSMA와 3GPP SA3에 보고해, 3GPP가 5G 펨토셀 보안 강화를 위한 연구 항목과 보안 보증 규격 작업 항목을 승인하는 성과로 이어졌습니다.

### Evaluation
- 인터넷 측정에서 발견된 기기를 군집화한 결과 한국통신(Korea Telecom)이 52,513대(60.99%)로 가장 많았고, 103개국에 분포하며 한국이 61.05%로 1위였습니다.
- 취약점은 실제 기기 분석으로 확인했고 코어망 공격은 실제 통신망에서 검증했으나, 측정에서 "펨토셀 의심"으로 분류한 기기는 배너와 포트 특징 기반 추정이라 일부 오분류 가능성이 있습니다.
- 윤리적 고려와 공개 절차를 별도 절로 서술했습니다.

#### Comment
- 한국 통신망에 배치된 펨토셀이 측정 대상의 60% 이상을 차지해, 국내 이동통신 인프라 보안에 직접적인 함의가 있습니다.
- 중국 기관 검증: 칭화대 두안하이신 교수 연구실이 주도하고 케이블랩스, 칼턴대와 공동 수행했으며, 치안신(QI-ANXIN) 기술연구소가 참여했습니다. 이 연구실은 네트워크 측정 분야 최상위 학회 실적이 꾸준하고, 결과가 GSMA/3GPP 표준 작업으로 이어진 점이 외부 검증 역할을 합니다. 측정 방법과 윤리 절차가 투명해 포함했습니다.
