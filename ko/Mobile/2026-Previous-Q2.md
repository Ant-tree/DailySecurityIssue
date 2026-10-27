2026년 2분기(4~6월)에 정식 게재된 학회 및 저널 논문 가운데 모바일 분류에 해당하는 논문 8편을 정리했습니다. 프리프린트(arXiv, IACR ePrint)는 제외했습니다.

- 악성코드 및 분석 (2)
- 프라이버시 (4)
- 그 외 (2)

---

**세부 분류: 악성코드 및 분석**

# MalPurifier: Enhancing Android Malware Detection With Adversarial Purification Against Evasion Attacks
> IEEE Transactions on Dependable and Secure Computing (TDSC), 저널 게재
> 2026

머신러닝 기반 Android 악성코드 탐지기는 비기능 명령을 조작해 만든 적대적 예제에 의한 회피 공격에 취약합니다. MalPurifier는 이 문제를 겨냥한 적대적 정제 프레임워크로, 다양한 범위의 변이를 주입해 강건성과 일반화를 높이고, 정상 데이터에는 보호용 잡음을 주입하며, 재구성 손실과 예측 손실을 함께 쓰는 디노이징 오토인코더(DAE)로 정제와 분류를 수행합니다.

원문: https://arxiv.org/abs/2312.06423 (저널판: IEEE TDSC, 2026)

### Contribution
- Android의 이산 특징 공간과 다양한 공격 벡터에 맞춘 정제 프레임워크를 제안하고, 전혀 주입하지 않는 경우부터 최악의 변이까지 다양하게 주입해 미지의 공격에 대한 강건성을 높입니다.
- 라벨 공간과 탐지 모델에 독립적인 DAE 기반 정제 모델을 두어, 탐지기에 끼워 넣는 경량·모델 비의존 모듈로 동작합니다.

### Evaluation
- Drebin과 AndroZoo 두 대규모 데이터셋에서 37종의 변이 기반 회피 공격을 막아 90.91% 이상의 강건 정확도를 유지했습니다.
- 정상 데이터에서는 Drebin 2.55%, AndroZoo 2.30%의 낮은 오탐률을 보여, 깨끗한 데이터 정확도 손실은 각각 1.72%, 0.66%로 작았습니다.
- 공개 데이터셋과 공개 코드(arXiv 전문 포함)로 재현 가능하며, 다수의 최신 방어와 비교해 판단 근거가 명확합니다.

#### Comment
- 적대적 정제를 탐지기와 분리된 플러그인 모듈로 두는 설계는, 운영 중인 Android 악성코드 탐지 엔진에 방어를 더할 때 그대로 참고할 만합니다.
- 중국 기관 검증: 둥난대(저우위양, 청광) 등의 연구로, 게재처 IEEE TDSC는 보안 분야 최상위 저널입니다. arXiv에 전문이 공개돼 실험 상세(데이터셋 구성, 비교 방어, 수치)를 직접 확인했고, 코드와 공개 데이터셋을 쓰며 수치가 과장 없이 트레이드오프를 밝혀 포함했습니다.

---

# Understanding Concept Drift With Deprecated Permissions in Android Malware Detection
> IEEE Transactions on Dependable and Secure Computing (TDSC), 저널 게재
> 2026

Android 권한 체계는 권한이 폐기되거나 제한되거나 시스템 전용으로 바뀌며 진화하고, 이는 악성코드 탐지의 특징 공간을 바꿔 개념 변화(concept drift)를 일으킵니다. 이 논문은 7만 개가 넘는 앱과 166개 권한으로 이런 변화가 머신러닝 모델에 미치는 영향을 연구합니다.

원문: IEEE TDSC, 2026

### Contribution
- 폐기·제한·시스템 전용 권한의 변화가 탐지 특징 공간에 일으키는 개념 변화를 대규모 데이터로 체계적으로 분석했습니다.
- 시간 요소를 고려한 권한 선택과 데이터셋 균형화가 탐지 성능에 미치는 영향을 정량화합니다.

### Evaluation
- (초록 기준 정리입니다. 전문을 확보하지 못해 세부 수치는 일부만 확인했습니다.) 시간을 고려하지 않고 제한 권한을 제거하면 정확도가 1.3~2.1%p 떨어지는 반면, 폐기·비제3자 권한 제외는 영향이 미미했습니다. 한 해로 학습해 다른 해로 시험할 때 데이터셋 균형화가 F1을 높였습니다.

#### Comment
- 권한 기반 Android 악성코드 탐지 모델을 운영할 때, 권한 체계 변화가 장기적으로 탐지 성능을 침식한다는 점을 보여 주는 실무적 참고 자료입니다.
- 게재처 IEEE TDSC는 보안 분야 최상위 저널입니다. 이 항목은 전문을 열지 못해 초록 기준으로 정리했으므로, 세부 평가는 원문 확인이 필요합니다.

---

**세부 분류: 프라이버시**

# Exercising the CCPA Opt-out Right on Android: Legally Mandated but Practically Challenging
> PoPETs 2026 Issue 2 (Privacy Enhancing Technologies Symposium), 저널형 학회
> 2026

많은 모바일 앱의 수익 모델은 광고 네트워크와 사용자 데이터를 공유하는 데 기대고, 캘리포니아 소비자 프라이버시법(CCPA)은 주민에게 이 공유를 거부할 권리를 줍니다. 이 논문은 인기 Android 앱이 실제로 이 권리를 얼마나 보장하는지 두 실험으로 평가합니다. 앱 자체 UI로 수동 거부를 시도한 첫 실험에서는 100개 앱 중 48개만 해당 설정을 제공했고, Global Privacy Control(GPC) 신호를 자동으로 보낸 둘째 실험에서는 1,811개 앱 데이터셋에서 GPC가 대체로 무효했습니다.

원문: https://petsymposium.org/popets/2026/popets-2026-0065.pdf

### Contribution
- CCPA 거부권이 Android 플랫폼에서 앱 수준과 플랫폼 수준 어디에서도 실효성 있게 행사되지 못한다는 준수 격차를 실측으로 드러냈습니다.
- Android 광고 ID(AdID) 설정을 CCPA 거부권 설정으로 재정의하면 이 격차를 메울 수 있다는 구체적 제안을 제시합니다.

### Evaluation
- 95% 신뢰수준에서 데이터셋 앱의 62~81%가 CCPA 거부권을 존중해야 한다고 추정되지만 다수가 그러지 않았습니다. GPC 신호를 보내고 AdID 접근을 차단해도, 광고 네트워크 Vungle 기준 338개 앱이 여전히 opted_in 상태였고 opted_out은 26개에 그쳤습니다.
- 두 실험 모두 실제 앱과 트래픽 측정에 기반해 판단 근거가 명확합니다. 결과는 측정 시점의 앱 버전과 광고 네트워크 동작에 의존합니다.

#### Comment
- 광고 ID와 추적 식별자를 다루는 모바일 보안 관점에서, 플랫폼 설정과 법적 권리 사이의 간극을 보여 주는 실증 자료로 유용합니다.
- 웨슬리언대와 마스트리흐트대 공동 연구이며, 공개 PDF와 GitHub 코드를 갖춘 PoPETs 게재 논문입니다.

---

# FreeLens: Revealing Mobile App Feature Differences and Their Security and Privacy Implications Across Geographical Regions
> IEEE Transactions on Dependable and Secure Computing (TDSC), 저널 게재
> 2026

모바일 앱은 지역 규제와 시장 선호에 맞춰 지역별로 다른 버전을 배포합니다. 기존 연구가 권한이나 프라이버시 정책 같은 메타데이터 차이를 다룬 반면, 이 논문은 보안에 영향을 줄 수 있는 코드 구현 수준의 지역별 차이(GFD)를 처음으로 체계적으로 조사합니다. FreeLens는 코드 난독화와 분석 확장성 같은 난제를 넘어 이런 차이를 식별하는 프레임워크입니다.

원문: IEEE TDSC, 2026

### Contribution
- Android 앱의 코드 구현 수준 지역별 차이를 처음으로 체계적으로 연구했습니다.
- 코드 난독화와 대규모 분석의 어려움을 극복해 지역별 기능 차이를 식별하는 프레임워크 FreeLens를 제안합니다.

### Evaluation
- (초록 기준 정리입니다. 전문을 확보하지 못해 데이터셋 규모와 세부 수치는 확인하지 못했습니다.) 초록은 코드 수준 지역 차이를 식별하고 그 보안·프라이버시 함의를 분석하는 수준까지 제시합니다.

#### Comment
- 지역별로 다른 앱 버전이 보안·프라이버시 격차를 만들 수 있다는 점은, 다국가 배포 SDK를 다루는 입장에서 참고할 만합니다. 코드 난독화를 분석 난제로 다룬다는 점도 흥미롭습니다.
- 게재처 IEEE TDSC는 최상위 저널입니다. 이 항목은 초록 기준이므로 세부 평가는 원문 확인이 필요합니다.

---

# PriLabel: Toward Comprehensively Uncovering Omitted Disclosures in Privacy Labels of Android Apps on a Large Scale
> IEEE Transactions on Information Forensics and Security (TIFS), 저널 게재
> 2026

프라이버시 라벨(예: Google Play의 데이터 안전 섹션)은 긴 프라이버시 정책을 간결하고 표준화된 요약으로 대체하려는 장치입니다. 그러나 자가 보고 라벨에는 누락과 왜곡이 많다는 연구가 이어졌습니다. 이 논문은 증거 기반으로 맥락을 재구성하는 Iterative Context Reconstruction(ICR) 워크플로로 이런 불일치를 대규모로, 라벨 감사의 의미적 모호성까지 다루며 찾아내려 합니다.

원문: IEEE TIFS, 2026

### Contribution
- 기존 방법이 부족했던 커버리지와 확장성, 그리고 라벨 감사의 의미적 모호성을 함께 겨냥한 ICR 워크플로를 제안합니다.
- 프라이버시 라벨의 누락 공개를 대규모로 체계적으로 들춰냅니다.

### Evaluation
- (초록 기준 정리입니다. 전문을 확보하지 못해 데이터셋과 정확도 수치는 확인하지 못했습니다.)

#### Comment
- 앱의 데이터 수집 실태와 공개 라벨의 괴리를 대규모로 감사하는 접근은, 모바일 프라이버시 준수와 SDK 데이터 흐름을 다루는 입장에서 참고가 됩니다.
- 게재처 IEEE TIFS는 최상위 저널입니다. 이 항목은 초록 기준이므로 세부 평가는 원문 확인이 필요합니다.

---

# SentinelTouch: A Lightweight Privacy-Preserving Biometric-Fingerprinting Authentication and Identification System Based on Neural Networks and Homomorphic Encryption
> PoPETs 2026 Issue 2 (Privacy Enhancing Technologies Symposium), 저널형 학회
> 2026

지문은 유출되면 바꿀 수 없어 안전한 저장과 연산이 중요합니다. 동형암호(HE)는 암호화된 상태로 연산해 강한 프라이버시를 보장하지만, 지문 이미지의 높은 차원과 신경망의 복잡도 때문에 실용화가 어려웠습니다. SentinelTouch는 지문 이미지를 28×28까지 줄이면서도 변별 정보를 보존하는 전처리와, 이 압축 데이터에서 잘 일반화되는 HE 친화적 경량 신경망을 결합한 공개 프레임워크입니다.

원문: https://petsymposium.org/popets/2026/popets-2026-0041.pdf

### Contribution
- 지문 차원 축소와 HE 친화 경량 신경망이라는 두 최적화로, 암호화 상태의 지문 인증과 식별을 실용 수준으로 끌어올렸습니다.
- 완전 프라이버시 파이프라인과 임베딩만 암호화하는 하이브리드 파이프라인을 모두 제시하고 공개했습니다.

### Evaluation
- 완전 프라이버시 파이프라인은 일대다 식별을 16초에, 하이브리드는 284밀리초에 수행해, 최신 결과 대비 각각 10배와 2.5배 속도 향상을 보고합니다.
- SOKOTO와 PolyU 데이터셋에서 Rank-1 정확도가 선도 암호화 시스템과 ±0.1% 이내였습니다.
- 공개 지문 데이터셋 기준 평가로 재현 가능하며, 실제 모바일 센서에서 수집한 지문이 아니라 공개 데이터셋 이미지를 쓴 점은 감안해야 합니다.

#### Comment
- 생체 정보를 기기 밖으로 내보내야 하는 클라우드·서버 인증에서 동형암호를 실용 지연 범위로 낮춘 사례로, 온디바이스 또는 서버 연동 생체 인증 설계에 참고가 됩니다.
- 애리조나주립대 STAM 센터의 논문으로, 코드가 GitHub에 공개된 PoPETs 게재 논문입니다.

---

**세부 분류: 그 외**

# Can Vibration Patterns Identify Users? Authentication for Smartphone-Watch Collaboration
> IEEE Transactions on Dependable and Secure Computing (TDSC), 저널 게재
> 2026

비밀번호나 지문 같은 전통적 인증은 위조와 재전송 공격에 취약합니다. 이 논문은 자연스러운 터치 동작에서 손과 손목으로 전파되는 능동 진동 신호의 특성에 주목해, 개인마다 다른 손목 구조와 미세 동역학이 안정적이고 구별 가능한 진동 응답으로 나타남을 밝힙니다. 이를 바탕으로 스마트폰과 스마트워치 양쪽을 쓰는 이중 단말 인증 시스템 VIP를 제안합니다. 양쪽 모터로 진동을 만들고 가속도계, 자이로스코프, 자력계로 응답을 수집해 TouchFormer 모델로 식별합니다.

원문: IEEE TDSC, 2026 (전문 확인)

### Contribution
- 스마트폰과 스마트워치의 능동 진동을 함께 쓰는 인증 시스템 VIP를 제안하고, 별도 하드웨어 없이 상용 기기에 바로 배포할 수 있게 설계했습니다.
- 다축·교차 모달·비동기 조건에서 방향 민감 특징을 뽑는 TouchFormer 모델을 설계해 다중 신호를 융합합니다.
- 성별, 나이, 체형이 다른 사용자와 다양한 상호작용 시나리오(착용 조임, 손바닥 습도 등)로 실측 데이터셋을 구성했습니다.

### Evaluation
- 상용폰 4종과 Redmi Watch 5에서 30명의 정상 사용자와 7명의 사칭 공격자로 4개월간 데이터를 수집했고(IRB 승인), TouchFormer가 평균 98.65% 정확도로 기존 기법을 앞섰습니다.
- 모의 공격과 재전송 공격에서의 오수용률이 각각 1.55%, 2.71%로 기존 대비 평균 0.61, 0.28%p 낮았습니다. 진동 세기 60%에서 FAR 0.34%, FRR 1.35%로 최적이었습니다.
- 사용자 30명 규모의 실측이라 대규모 일반화는 추가 검증이 필요하고, 5겹 교차검증으로 평가 신뢰도를 보완했습니다.

#### Comment
- 웨어러블과 스마트폰을 묶은 행동 생체 인증은 모바일 런타임 보호와 사용자 인증 설계에 참고가 됩니다. 센서 응답 기반이라 기기 하드닝 관점에서도 흥미롭습니다. 세 모바일 세부 분류에 정확히 들지 않아 그 외로 넣었습니다.
- 중국 기관 검증: 창안대, 시안자오퉁대, 지난대와 영국 에식스대, 호주 에디스코완대 공동 연구입니다. 게재처 IEEE TDSC는 최상위 저널이고, 전문을 확인해 IRB 승인, 교차검증, 공격 시나리오별 수치 등 방법론이 구체적이며 결과가 과장 없이 제시돼 포함했습니다.

---

# Security risk assessment of android automotive OS software supply chain using firmware reverse engineering
> Computers & Security (Elsevier), 저널 게재
> 2026

Android Automotive OS(AAOS)는 현대 승용차의 인포테인먼트와 도메인 컨트롤러 기능을 담당하는 차량 내 플랫폼으로 자리잡고 있습니다. 미디어 스트리밍, 무선 업데이트, 내비게이션, 센서 융합을 지원하면서 인포테인먼트와 차량 제어 영역을 아우릅니다. 오픈소스 기반과 제3자 라이브러리 의존성은 오래된 구성 요소나 악성 모듈 같은 위험을 들여오고, 이는 차량 기능과 승객 안전을 위협할 수 있습니다. 이 논문은 펌웨어 역공학으로 AAOS 소프트웨어 공급망의 보안 위험을 평가합니다.

원문: Computers & Security, 2026

### Contribution
- AAOS의 소프트웨어 공급망을 펌웨어 역공학 관점에서 보안 위험 평가 대상으로 다룹니다.
- 인포테인먼트와 차량 제어를 아우르는 플랫폼에서 오래된 구성 요소와 제3자 라이브러리 위험을 짚습니다.

### Evaluation
- (초록 기준 정리입니다. 전문을 확보하지 못해 분석 대상 펌웨어 수와 세부 결과는 확인하지 못했습니다.)

#### Comment
- 차량용 Android 플랫폼의 공급망과 펌웨어 역공학을 다룬다는 점에서, 모바일·임베디드 하드닝과 바이너리 분석 관점의 확장 주제로 흥미롭습니다. 모바일 세부 분류에 정확히 들지 않아 그 외로 넣었습니다.
- 게재처 Computers & Security는 보안 분야의 평판 있는 저널입니다. 이 항목은 초록 기준이므로 세부 평가는 원문 확인이 필요합니다.
