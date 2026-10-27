2026년 3분기(7~9월)에 정식 게재된 학회 및 저널 논문 가운데 AI 보안 분류에 해당하는 논문 4편을 정리했습니다. 프리프린트(arXiv, IACR ePrint)는 제외했습니다.

---

# Measuring Real-World Prompt Injection Attacks in LLM-based Resume Screening
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

LLM이 이력서 심사에 쓰이면서, 지원자가 이력서에 심은 지시문이 심사 모델을 조종하는 프롬프트 주입이 실제로 일어납니다. 이 논문은 LLM 기반 이력서 심사에서 이런 현실의 프롬프트 주입 공격을 측정해, 공격이 얼마나 퍼져 있고 어떤 형태인지, 그리고 실제 심사 결과에 어떤 영향을 주는지를 분석합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/zhang-mohan

### Contribution
- 이력서 심사라는 구체적 응용에서 프롬프트 주입의 실제 발생과 효과를 측정했습니다.
- 공격이 심사 결과를 유리하게 바꾸는 정도를 정량화해, 실무에서의 위협을 구체적 근거로 제시합니다.

### Evaluation
- LLM 기반 이력서 심사 환경에서 프롬프트 주입의 발생과 영향을 측정하는 방식으로 평가합니다. 공개 PDF로 방법을 확인할 수 있습니다.
- 특정 응용(채용)에 초점을 맞춘 측정이라, 결과의 일반화는 심사 파이프라인 구성에 따라 달라질 수 있습니다.

#### Comment
- 외부 입력(이력서)이 LLM 판단을 조종하는 전형적 간접 주입 사례로, 사용자 데이터를 LLM에 넣는 모든 모바일·서버 응용의 입력 신뢰 설계에 참고가 됩니다.
- UNC 채플힐, 듀크대, 애리조나주립대, UC 버클리 공동 연구이며 USENIX Security 게재 논문입니다.

---

# Overcoming the Retrieval Barrier: Indirect Prompt Injection in the Wild for LLM Systems
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

LLM 시스템이 외부 말뭉치에서 정보를 검색해 쓰면서 간접 프롬프트 주입이라는 새 공격면이 생깁니다. 기존 연구는 이 위험을 지적하면서도 "악성 내용이 실제로 검색되게 하는" 가장 어려운 단계를 피했습니다. 자연스러운 질의에서는 최적화되지 않은 주입이 거의 검색되지 않아 실제 영향이 불분명했습니다. 이 논문은 악성 내용을 검색을 보장하는 트리거 조각과 공격 목표를 담는 공격 조각으로 분리해, 검색 장벽을 넘는 효율적 블랙박스 공격을 설계합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/chang-hongyan

### Contribution
- 간접 프롬프트 주입에서 그동안 회피돼 온 "검색되게 만들기" 단계를 정면으로 다룹니다.
- 트리거 조각과 공격 조각을 분리해, 검색 보장과 공격 목표 전달을 모두 달성하는 블랙박스 공격 알고리즘을 제안합니다.

### Evaluation
- 검색 기반 LLM 시스템에서 주입 내용의 실제 검색률과 공격 성공을 함께 측정하는 방식으로 평가합니다. 공개 PDF로 방법을 확인할 수 있습니다.
- 검색 단계까지 포함한 현실적 위협 모델을 다룬다는 점이 기존 연구와의 차별점이며, 방어 관점에서 검색 단계의 중요성을 부각합니다.

#### Comment
- 검색 증강(RAG) 구조에서 주입이 실제로 검색돼야 위협이 성립한다는 점은, 외부 지식을 끌어오는 온디바이스·서버 LLM의 방어 설계에서 검색 단계를 함께 봐야 함을 보여 줍니다.
- 모하메드 빈 자이드 AI 대학교(MBZUAI)의 논문이며 USENIX Security 게재 논문입니다.

---

# SoK: Attack and Defense Landscape of Agentic AI Systems
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

이 체계화(SoK) 논문은 에이전트형 AI 시스템의 공격과 방어 지형을 시스템 관점에서 종합 정리합니다. 에이전트를 입력 신뢰, 접근 민감도, 워크플로, 행동, 메모리, 도구, 사용자 인터페이스라는 일곱 가지 설계 차원으로 특성화하고, 각 차원의 유연성이 보안 위험에 어떻게 영향을 주는지 분석합니다. 방어는 런타임 보호, 설계 단계 보안, 구성 요소 하드닝 세 범주로 나눠 정리합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/

### Contribution
- 에이전트형 AI 시스템을 일곱 가지 설계 차원으로 특성화하는 체계적 틀을 제시하고, 각 차원의 유연성과 보안 위험의 관계를 분석합니다.
- 방어 기법을 런타임 보호, 설계 단계 보안, 구성 요소 하드닝으로 분류하고 구체적 설계 차원과 열린 과제를 짚습니다.
- 에이전트 보안을 종합적 시스템 관점에서 처음으로 체계 분석했다고 밝힙니다.

### Evaluation
- 공격과 방어를 설계 차원 기준으로 분류·대조하는 체계화 연구로, 개별 기법의 실측보다 전체 지형의 구조화에 초점을 둡니다.
- 에이전트 보안 위험과 방어 전략을 이해하는 기초 틀을 제공합니다.

#### Comment
- 1분기의 ACE, SAGA 같은 에이전트 보안 구조 연구를 포괄하는 지형도로, 온디바이스 에이전트의 위협 모델과 방어 설계를 정리할 때 출발점으로 삼기 좋습니다.
- USENIX Security 게재 논문입니다.

---

# Patcher: Post-Hoc Patching of Backdoored Large Language Models
> USENIX Security 2026 (35th USENIX Security Symposium), 2026년 8월 발표
> 2026

대형 언어 모델은 학습 과정에 심긴 백도어로 특정 트리거에서 공격자가 의도한 출력을 내도록 조작될 수 있습니다. Patcher는 이미 백도어가 심긴 LLM을 사후에 패치해 백도어 동작을 무력화하려는 방어 기법입니다. 모델을 처음부터 다시 학습하지 않고 배포 후 단계에서 백도어를 제거하는 것을 목표로 합니다.

원문: https://www.usenix.org/conference/usenixsecurity26/presentation/gao-anjun

### Contribution
- 백도어가 심긴 LLM을 재학습 없이 사후에 패치해 백도어를 제거하는 방어를 제안합니다.
- 배포 이후 단계에서 적용 가능한 방어라는 점에서 실무적 적용성을 지향합니다.

### Evaluation
- (전문을 받았으나 요약 다이제스트에서 세부 수치가 충분히 추출되지 않았습니다. 평가는 여러 백도어 공격에 대한 제거 효과와 정상 성능 유지를 측정하는 방식으로 구성됩니다.)
- 사후 패치라는 접근은 재학습 비용이 큰 대형 모델에 현실적이며, 구체 수치는 원문 확인을 권합니다.

#### Comment
- 공개 가중치 모델을 받아 쓰는 환경에서 백도어 위험을 배포 후 완화한다는 점은, 온디바이스나 사내에서 외부 LLM을 가져다 쓰는 입장에 직접적인 함의가 있습니다.
- 루이빌대와 노스텍사스대 공동 연구이며 USENIX Security 게재 논문입니다.
