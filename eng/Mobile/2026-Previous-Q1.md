This file covers 18 peer-reviewed conference and journal papers in the Mobile category published in Q1 2026 (January to March). Preprints (arXiv, IACR ePrint) are excluded.

- Malware and Analysis (1)
- On-Device LLMs (1)
- Privacy (7)
- TEEs and Side Channels (2)
- Other (7)

---

**Subcategory: Malware and Analysis**

# CHAMELEOSCAN: Demystifying and Detecting iOS Chameleon Apps via LLM-Powered UI Exploration
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

The paper studies iOS "chameleon" apps, which look harmless during App Store review but turn into gambling or other illicit apps once a user performs an action the developer shares through unofficial channels. The authors analyze these apps at scale, sort their transformation methods into 10 categories (four of them newly reported), and propose CHAMELEOSCAN. The system infers candidate transformation methods from App Store metadata and user reviews, then uses a multimodal LLM to understand real screens, perform interactions, and confirm whether the app transforms.

Paper: https://www.ndss-symposium.org/ndss-paper/chameleoscan-demystifying-and-detecting-ios-chameleon-apps-via-llm-powered-ui-exploration/

### Contribution
- It is the first systematic account of how collusion-based chameleon apps transform and how they are distributed.
- Unlike the earlier static tool Chameleon-Hunter, it confirms transformations by actually running the app and exploring its UI, which also covers apps built on dynamically rendered UI.
- It delegates distraction handling (ads, pop-ups) and UI element recognition to an LLM, automating UI exploration at close to human granularity.

### Evaluation
- On a ground-truth set of 131 chameleon apps and 233 benign apps, it reached 100% precision and 71.76% recall; recall rises to 96.91% for apps whose reviews mention the transformation.
- Recall was 95% for auto-transforming apps and 100% for time- and location-conditioned apps, but lower for types with few metadata hints, such as input-based ones.
- GPT-4o is the underlying model. The authors call the system model-agnostic but report no results with other models. The ground-truth set is small, so the 100% precision should be generalized with care.

#### Comment
- Detection leans heavily on external hints such as user reviews, so it is likely to be weaker on new apps with no reviews.
- A practical example of applying LLM-driven dynamic UI exploration to app vetting and disguised-app detection.
- Verification of a Chinese institution: the work is led by Zhejiang University with co-authors from Old Dominion University and the Colorado School of Mines. Code is on GitHub and the results are reported candidly, including uneven recall across types, so the paper is included.

---

**Subcategory: On-Device LLMs**

# PhishLang: A Real-Time, Fully Client-Side Phishing Detection Framework Using MobileBERT
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

PhishLang is a Chromium extension that detects phishing sites in real time on the user's own device using the lightweight language model MobileBERT. Heuristic and static-feature models struggle with evasive phishing, while large deep learning models are too heavy for the client, so the authors train the model directly on the contextual structure of page source code. It matches several state-of-the-art models while using up to 7 times less memory, and during 3.5 months of live operation it found about 26,000 phishing URLs that blocklists had missed.

Paper: https://www.ndss-symposium.org/ndss-paper/phishlang-a-real-time-fully-client-side-phishing-detection-framework-using-mobilebert/

### Contribution
- The first practical language-model-based phishing detector that runs entirely on the client without server lookups; both the framework and the extension are open source.
- It hardens the model against 16 realistic problem-space evasions, including JavaScript evasion, clickjacking, DOM manipulation, and text encoding, by combining parser-level defenses with adversarial retraining.
- Detections were reported to blocklist operators right away, with measurable ecosystem gains: for example, Google Safe Browsing's detection of JavaScript-evasion attacks rose from 35% to 73%.

### Evaluation
- From September 2023 to January 2024 it scanned 42.7 million domains from Certstream and flagged 25,796 as phishing. Two coders manually checked 2,500 random detections and found 95.5% precision (Cohen's kappa 0.82).
- It detected over 91% of threats at zero-day, ahead of several existing tools.
- Misses were studied through 261 sites found via VirusTotal, mostly due to CAPTCHAs and QR codes. Recall was measured only against VirusTotal, not against the whole population.

#### Comment
- Strictly speaking it is a browser extension, but its design of making security decisions with a small client-side language model carries over directly to on-device detection engines on phones, which is why it is filed under on-device models.
- From the University of Texas at Arlington, published at NDSS.

---

**Subcategory: Privacy**

# ANONYCALL: Enabling Native Private Calling in Mobile Networks
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Mobile operators manage subscribers through permanent identifiers such as phone numbers and SUPIs, which lets them track location and call history. Several anonymous network-access schemes already let a device attach without exposing those identifiers, but none of them explains how such a device can receive calls or be billed for usage. ANONYCALL is a call-management architecture that provides both functions without breaking anonymity. A caller authenticates out of band through the callee's authentication agent, obtains the callee's temporary SIP URI, and places an ordinary VoLTE or VoNR call. Billing relies on an anonymous balance credential combined with zero-knowledge proofs that prevent double spending.

Paper: https://www.ndss-symposium.org/ndss-paper/anonycall-enabling-native-private-calling-in-mobile-networks/

### Contribution
- It solves callee discovery and usage-based charging together, the two pieces earlier anonymous-access work left open, which brings anonymous access closer to a usable telecom service.
- On the call path the operator only sees a temporary SIP URI and an internal IP, so sessions cannot be linked. On the billing side, SPS-EQ-based credentials and range proofs let the device prove its usage without becoming traceable.
- It requires no changes to the IMS architecture or SIP messages, so it could be deployed without modifying standard protocols.

### Evaluation
- The authors demonstrate calls between two real phones using an open5gs core with IMS, an Android prototype app, and an authentication agent hosted on AWS. Fetching a temporary SIP URI took about 80 ms over Wi-Fi, the full flow including authentication took 50 to 180 ms, and the added call-setup latency stayed under 200 ms.
- The billing protocol's client and server computation was measured on the bn254 curve with the Cryptimeleon and mcl libraries.
- The latency figures come from a small prototype and depend heavily on network conditions; operator-scale load and many concurrent users were not tested. Security is backed by proof sketches rather than experiments.

#### Comment
- This follows the line of anonymous-access work (USENIX Security 2021, NDSS 2024, CCS 2024, S&P 2025). Its main limitation is that the anonymous-access schemes it builds on have not been deployed in commercial networks.
- The paper says little about why an operator would adopt the design beyond billing support, so it is best read as a feasibility study.
- Joint work by Virginia Tech, the University of Kentucky, and Georgia Tech, published at NDSS, a top-tier security venue. Prototype code is available on Zenodo.

---

# Connecting the Dots: An Investigative Study on Linking Private User Data Across Messaging Apps
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

People often run KakaoTalk, Telegram, WhatsApp, Signal, and Tinder on the same phone. This study asks what privacy threats arise when contact discovery, SSO-based account linking, and nearby-user search in these apps are combined. The authors first identify how each app leaks personal data, then chain those leaks into the first cross-platform linking attack: a user who is anonymous on one platform can be matched to a real-name profile on another, and their location can be estimated. Phone numbers and profile pictures turn out to be the keys that tie platforms together.

Paper: https://www.ndss-symposium.org/ndss-paper/connecting-the-dots-an-investigative-study-on-linking-private-user-data-across-messaging-apps/

### Contribution
- It extends messaging-app privacy research from single apps to the realistic case of several apps used side by side, where information can be combined.
- It shows through measurement that KakaoTalk's contact-registration budget is permissive enough to identify phone-number owners at scale, and that 63 popular websites expose Kakao SSO tokens in URLs or browser storage.
- It argues for stricter contact-discovery policies and proposes platform-specific mitigations.

### Evaluation
- An account backed by a single phone number was enough to collect more than 105,000 KakaoTalk profiles, with a 67.9% success rate.
- Cross-referencing Telegram with KakaoTalk, 70 of the 88 Telegram users found among 1,000 random numbers (79.55%) were matched to real-name profiles.
- Tinder location inference reached an average error of 385 m with 12 queries and 324 m with 40, far more efficient than prior work that needed 676 queries for similar accuracy. The location experiment used only 10 random locations, though.

#### Comment
- It is one of the few studies that tackles the Korean messaging landscape directly, especially KakaoTalk, which covers 94% of the population. The introduction cites anonymous chat-room users whose phone numbers were later used for voice phishing as motivation.
- Results reflect platform policies at measurement time, which may have changed after disclosure.
- Joint work by KAIST and the University of Maryland, published at NDSS.

---

# Cross-Boundary Mobile Tracking: Exploring Java-to-JavaScript Information Diffusion in WebViews
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Android WebViews run web content in an isolated, browser-like context, but apps can cross that boundary by injecting JavaScript at runtime or exposing Java methods to JavaScript. Existing tools either analyze only the app's Java code or have little visibility into JavaScript running inside WebViews. The authors build WebViewTracer, a dynamic analysis system that combines JavaScript execution traces inside WebViews with Java method-call information, and run it on 10,000 Android apps. Of the 4,597 apps that load WebViews, more than 69% inject information JavaScript normally cannot reach, such as the Advertising ID or the build ID, and 90% of those send it to third-party servers through web APIs.

Paper: https://www.ndss-symposium.org/ndss-paper/cross-boundary-mobile-tracking-exploring-java-to-javascript-information-diffusion-in-webviews/

### Contribution
- An open-source tool that pairs VisibleV8-based JavaScript tracing with Frida-based Java hooking to follow information from Java into JavaScript end to end.
- The first large-scale measurement of cross-context information diffusion, showing that the WebView isolation model is being eroded in practice for advertising and tracking.
- Stack-trace attribution shows that most injections come from third-party libraries rather than the app itself.

### Evaluation
- 96% of injections came from third-party libraries bundled in the app and only 3.6% from first-party code. 53% of WebView-using apps injected build IDs, and 23.30% of WebViews received the Advertising ID. Ad SDKs such as Unity and ironSource were the main sources.
- The authors acknowledge that their automated UI exploration reached only about half the WebViews found through manual interaction, so the figures should be read as lower bounds.
- Manual analysis of popular apps such as Facebook and Instagram turned up seven new injection types and nine Java-to-JavaScript bridges not reported in earlier work.

#### Comment
- For teams building app security SDKs, the paper provides concrete evidence that WebView bridges (addJavascriptInterface, evaluateJavascript) act as a channel for leaking device identifiers, mostly driven by ad SDKs.
- Joint work by NC State, the Technical University of Crete, and the University of Illinois Chicago; the tool is on GitHub.

---

# Hey there! You are using WhatsApp: Enumerating Three Billion Accounts for Security and Privacy
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Messengers let users find contacts by checking which phone numbers in their address book are registered, and that design inherently enables phone-number enumeration. This paper shows that WhatsApp's rate limiting was effectively absent: the authors could query more than 100 million numbers per hour without being blocked, and they confirmed all 3.5 billion active accounts. About half of the numbers from the 2021 Facebook leak were still active on WhatsApp, and some X25519 public keys were reused across different devices and numbers.

Paper: https://www.ndss-symposium.org/ndss-paper/hey-there-you-are-using-whatsapp-enumerating-three-billion-accounts-for-security-and-privacy/

### Contribution
- A method that uses the numbering plans of 245 countries to narrow the space of assignable mobile numbers to about 63 billion candidates.
- It shows that even with end-to-end encrypted messages, contact discovery alone reveals macroscopic data such as users per country, growth and churn, OS shares, and companion-device usage.
- It finds identical public keys used by different accounts, pointing to faulty unofficial clients or fraudulent activity.

### Evaluation
- The results are real measurements. The authors state that they did not analyze individuals and report only aggregate statistics, such as companion-device rates by country (over 22% in the Netherlands and Israel, under 3% in some countries) and monthly churn (under 1% in Belgium, 2% in India).
- The disclosure process with Meta is documented date by date, and Meta's official statement in the final version says mitigations are under way.
- Accuracy is not really the question for a measurement like this; credibility rests on how complete the coverage is. The dataset is not released.

#### Comment
- Being able to check registration, profile picture, and status text from a phone number alone could directly help smishing and voice-phishing campaigns pick targets, which makes this relevant to mobile fraud defense.
- Releasing a preprint before a fix may be controversial, but the authors explain their reasoning openly.
- Joint work by the University of Vienna and SBA Research, published at NDSS.

---

# MVPNalyzer: An Investigative Framework for Auditing the Security & Privacy of Mobile VPNs
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

VPN apps intercept all of a user's traffic, so trust simply moves from the network operator to the VPN provider. Mobile VPN apps, however, are rarely audited. The authors build MVPNalyzer, an extensible framework that analyzes Android VPN apps across network layers, and apply it to 281 popular VPN apps from Google Play. They find that 61 apps send unencrypted data (five of them send VPN configuration files in cleartext, allowing tunnel hijacking), 29 leak traffic including DNS outside the tunnel, and 76 transmit the Advertising ID.

Paper: https://www.ndss-symposium.org/ndss-paper/mvpnalyzer-an-investigative-framework-for-auditing-the-security-privacy-of-mobile-vpns/

### Contribution
- An analysis pipeline that installs, connects, and measures VPN apps on real devices and compares traffic inside and outside the tunnel. It also sets criteria for filtering out apps that use Android's VPN interface for other purposes, such as antivirus or DNS-changer apps.
- Results are organized along five axes: cleartext transmission, traffic leaks, traffic obfuscation against blocking, tracking identifiers, and OpenVPN configuration best practices.
- The affected apps add up to hundreds of millions of installs, which shows how widespread developer negligence is.

### Evaluation
- Apps were collected with 40 search terms plus the VPN category across all countries; 281 working apps that needed no account or payment were tested on a physical Android 14 device.
- The paper reports 10,552 cleartext flows, 143 apps without traffic obfuscation, 107 apps not following configuration best practices, and more than 80% of apps (246) contacting advertising and tracking domains.
- Decision rules are explicit, for example classifying an app as leaking when 90% or more of visited domains appear outside the tunnel, which makes replication easier. Paid and account-gated apps were excluded, so the sample does not represent the whole market.

#### Comment
- The finding that VPNs sold as security tools can become channels for identifier collection and cleartext traffic is useful when defining evaluation criteria for mobile security products.
- Joint work by the University of Michigan (Roya Ensafi's lab, well known for censorship and VPN measurement) and the University of New Mexico, published at NDSS.

---

# Passive Multi-Target GUTI Identification via Visual-RF Correlation in LTE Networks
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

LTE uses the temporary GUTI to avoid exposing the permanent IMSI. This paper shows that by matching camera-observed moments of device use with the timing of control-plane messages captured by commodity SDRs, an adversary who never transmits can identify the GUTIs of several devices in view at once. About three observed user interactions were enough. In some commercial networks GUTIs stayed unchanged for up to 33 days, and reassignments were often linkable. Once linked, a GUTI allows location tracking at cell or paging-area granularity just by listening to paging and RRC messages.

Paper: https://www.ndss-symposium.org/ndss-paper/passive-multi-target-guti-identification-via-visual-rf-correlation-in-lte-networks/

### Contribution
- Earlier GUTI attacks needed prior information such as a phone number and actively triggered paging. This work formalizes a listen-only threat model that identifies multiple targets in parallel.
- A finite-state-machine identification algorithm that recovers when some control messages are missed.
- Measurements of GUTI lifetimes and reassignment patterns in commercial networks, quantifying the gap between standard recommendations and operational practice. The issue was responsibly disclosed to GSMA.

### Evaluation
- Across 12 sessions on four operators in two countries, 36 of 37 per-device attempts (97%) succeeded in extraction and 35 (94%) were fully verified. A mix of iPhones and Samsung phones with Qualcomm and Exynos chipsets showed no chipset dependence.
- It worked even with about 16% control-packet loss, with sniffer processing rates between 73% and 100%.
- The number of targets and locations is limited, and the target devices were deliberately placed in the camera's view, so success rates in crowded public spaces still need separate validation.

#### Comment
- Where CCTV is already in place, a short video observation could become long-term RF tracking, which underlines how much operator policies such as GUTI reassignment intervals matter.
- Written by researchers at the National Security Research Institute (an affiliate of ETRI in Korea); a Korean institution's cellular security work appearing at NDSS.

---

# PriSrv+: Privacy and Usability-Enhanced Wireless Service Discovery with Fast and Expressive Matchmaking Encryption
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Wireless service discovery protocols such as Wi-Fi, BLE, and mDNS broadcast advertisements in cleartext, exposing devices to tracking, session linking, and impersonation. PriSrv+ improves on PriSrv (NDSS 2024) and is built around a new matchmaking encryption scheme, FEME. FEME supports expressive access policies in which any string can serve as an attribute, while hiding both messages and attribute values. Compared with PriSrv, encryption is 7.62 times faster, decryption 6.23 times faster, and ciphertexts are 87.33% smaller.

Paper: https://www.ndss-symposium.org/ndss-paper/prisrv-privacy-and-usability-enhanced-wireless-service-discovery-with-fast-and-expressive-matchmaking-encryption/

### Contribution
- FEME is the first matchmaking encryption scheme with an unbounded attribute universe, removing PriSrv's restriction to fixed binary attribute vectors.
- Revealing only attribute names while hiding their values keeps filtering fast without decryption and removes tracking risk.
- The protocol stays compatible with mDNS, BLE, and Wi-Fi, and cuts communication in the broadcast and anonymous mutual authentication phases by 87.33% and 86.64%. Formal security proofs are provided.

### Evaluation
- Computation and communication costs were compared against ACME on a desktop across three curves (MNT159, MNT201, BN256) using the same attribute counts and policies, and full-protocol performance was measured on several platforms.
- The comparison is fair in setup, but the curves offer 80 to 100 bits of security, below today's recommended 128-bit level.
- There is no large-scale deployment in a real wireless environment; the evaluation centers on microbenchmarks.

#### Comment
- As a cryptographic protocol paper, it is more useful as a design reference for private device discovery than as something ready to deploy.
- Led by Singapore Management University with the University of Oregon, Hainan University, and Jinan University. Verification of Chinese co-authors: Jian Weng (Jinan University) is a long-established applied cryptography researcher, and Robert Deng's group at SMU is well known. Code is on Zenodo and GitHub and the scheme comes with formal proofs, so the paper is included.

---

**Subcategory: TEEs and Side Channels**

# Side-channel Inference of User Activities in AR/VR Using GPU Profiling
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Earlier attacks in which a malicious AR/VR app spies on other apps assumed high-resolution performance counters and concurrent app execution, which does not work on devices such as Meta Quest that disable concurrent standalone apps. OVRWATCHER is a side channel that infers user activity by collecting only low-resolution (1 Hz) GPU metrics in the background through the device's built-in GPU profiler. Without extra SDKs or access to app data, it reveals which app is in use and even which products a user picks in a shopping app or how many people are in a virtual meeting.

Paper: https://www.ndss-symposium.org/ndss-paper/side-channel-inference-of-user-activities-in-ar-vr-using-gpu-profiling/

### Contribution
- The first demonstration of a low-resolution GPU side channel on AR/VR devices that needs no concurrent execution.
- A systematic analysis showing that, among 72 GPU metrics, texture mipmap metrics correlate strongly with the size, distance, and speed of on-screen 3D objects; correlation with pixel coverage reached 0.94 to 0.99 in VR mode.
- Disclosed through Meta's bug bounty program, which awarded the authors.

### Evaluation
- Fingerprinting the 100 most popular free Meta Quest apps reached 99.5% accuracy with a random forest, and a single metric already gave an F1 above 90%. Object-level inference exceeded 98%.
- Virtual objects selected by real participants were distinguished with up to 88% accuracy despite environmental noise, and a cross-device setting with limited metrics stayed above 93% in every case study.
- Each app was profiled 20 times in a controlled dataset, so real-world variety is only partly captured.

#### Comment
- XR headsets use the same kinds of SoCs as phones, and the paper shows that controlling access to GPU profiling APIs is central to defending against this class of side channel.
- Joint work by Iowa State, Purdue, and the American University of Sharjah, published at NDSS.

---

# XR Devices Send WiFi Packets When They Should Not: Cross-Building Keylogging Attacks via Non-Cooperative Wireless Sensing
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Earlier XR keystroke-inference attacks assumed line of sight or close proximity (under 10 meters). This paper presents a keylogging attack that uses Wi-Fi sensing to work without line of sight, across buildings, at up to 30 meters. The key is a Wi-Fi chipset vulnerability: when the attacker sends a forged unencrypted packet, the victim's device automatically returns an ACK. Repeating this forces the headset to keep transmitting, and the harvested Channel State Information is used to estimate hand and finger positions and infer keystrokes. Unlike prior Wi-Fi attacks, it needs no dedicated transmitter or fake hotspot.

Paper: https://www.ndss-symposium.org/ndss-paper/xr-devices-send-wifi-packets-when-they-should-not-cross-building-keylogging-attacks-via-non-cooperative-wireless-sensing/

### Contribution
- The first XR keylogging attack that works at long range without line of sight.
- It turns the headset itself into a transmitter, collecting large amounts of CSI without any network access, and removes the requirement that the victim sit between the attacker's transmitter and receiver.
- An unsupervised wireless-sensing method that estimates user motion without training data; the authors say they will open-source the implementation and data.

### Evaluation
- Evaluated on Meta Quest 2 and 3 across 1 to 30 meters, angles from -90° to +90°, through-wall, and multiple users. For 15-character passwords in a cross-building setting, it reports 78.6% top-25 accuracy.
- In the 30-meter cross-building test, top-1 was 16.30%, top-4 51.40%, and top-9 74.30%, so top-1 accuracy drops sharply with distance.
- Performance held up on unseen users and headsets, supporting generalization, but the low top-1 accuracy makes it closer to narrowing candidates than reconstructing input outright.

#### Comment
- It shows how a low-layer property of mobile and XR Wi-Fi chipsets, automatically acknowledging unencrypted packets, becomes a physical side channel, which is relevant from a device-hardening perspective.
- From UCLA, published at NDSS.

---

**Subcategory: Other**

# AirSnitch: Demystifying and Breaking Client Isolation in Wi-Fi Networks
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Client isolation blocks direct communication between devices on the same Wi-Fi network to stop insider attacks such as ARP spoofing. It is not standardized, though, so policies vary across implementations and its guarantees are unclear. This paper analyzes client isolation across three layers (Wi-Fi encryption, packet switching, and routing) and finds new attacks that bypass it. The root causes are mismanaged keys for broadcast frames, isolation enforced only at the MAC or IP layer but not both, and weak synchronization of a client's identity across the network stack. Every router and network tested was vulnerable to at least one attack.

Paper: https://www.ndss-symposium.org/ndss-paper/airsnitch-demystifying-and-breaking-client-isolation-in-wi-fi-networks/

### Contribution
- New attack primitives that break client isolation and enable full machine-in-the-middle capability over both uplink and downlink traffic.
- A demonstration that in single-BSSID home networks client isolation is fundamentally broken across all WPA versions.
- Extensions to higher-layer attacks, including intercepting traffic from wired internal devices and cracking weak back-end RADIUS passwords; the code is open-sourced.

### Evaluation
- Attacks were validated on five home routers from popular vendors, the open-source distributions DD-WRT and OpenWRT, and two real university networks.
- Isolation between virtual BSSIDs was often missing or misconfigured, while DD-WRT and OpenWRT with recommended settings blocked port stealing.
- Covering multiple vendors and real networks gives strong generalization, and artifacts on Zenodo and GitHub make it reproducible.

#### Comment
- It shows that client isolation, widely assumed safe in home and enterprise Wi-Fi, cannot really be trusted, which prompts rethinking the trust model of the wireless networks mobile devices join.
- Joint work by UC Riverside and KU Leuven (Mathy Vanhoef, a leading Wi-Fi security researcher), published at NDSS.

---

# BLERP: BLE Re-Pairing Attacks and Defenses
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

BLE security rests on pairing, which establishes a long-term key, and session establishment, which encrypts traffic with a session key. The standard lets already-paired devices re-pair to negotiate a new security level, but the security implications of re-pairing had not been examined. This paper analyzes re-pairing as defined in Bluetooth Core Specification v6.1, finds six design vulnerabilities (four new, such as unauthenticated re-pairing and security-level downgrade), and presents four attacks called BLERP. They enable device impersonation and machine-in-the-middle with little or no user interaction.

Paper: https://www.ndss-symposium.org/ndss-paper/blerp-ble-re-pairing-attacks-and-defenses/

### Contribution
- The first security analysis of BLE re-pairing, revealing design flaws that affect any standard-compliant device regardless of Bluetooth version or security level.
- An open-source attack and MitM testing toolkit reproducible on low-cost hardware (nRF52).
- Two defenses: an immediately deployable hardening of re-pairing, and an authenticated re-pairing protocol that fixes the issues by design, formally verified with ProVerif.

### Evaluation
- Attacks were validated on 22 targets, including 15 BLE hosts and 12 controllers, and remained effective on Bluetooth 4.2 to 5.4 and the most secure settings (SC, SCO, authenticated pairing).
- Implementation flaws were also found in the Apple, Android, and NimBLE stacks. The attacks are 0-click against devices with no I/O and 1-click against those with I/O.
- The authors note they could not test devices with the newest Bluetooth versions, as none were on the market.

#### Comment
- The Bluetooth SIG acknowledged the issues but does not plan to amend the standard; Apple (iOS/macOS 26), Google (Android 16), and Apache took mitigating steps. Because these are standard-level flaws, individual vendor patches will not fully resolve them.
- From EURECOM (Daniele Antonioli, a leading Bluetooth-security researcher), published at NDSS.

---

# BSFuzzer: Context-Aware Semantic Fuzzing for BLE Logic Flaw Detection
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

BLE's complex design produces subtle logic flaws, such as misinterpreted fields or invalid state transitions, that can lead to authentication bypass or denial of service and often escape conventional fuzzing and formal analysis. BSFuzzer is a black-box, semantic fuzzing framework that uses an LLM agent to parse the Bluetooth Core Specification into state machines and packet semantics, generates field-level and state-level mutations, and runs them on real devices. The LLM also checks whether responses match expected behavior, catching logic flaws that traditional fuzzers miss.

Paper: https://www.ndss-symposium.org/ndss-paper/bsfuzzer-context-aware-semantic-fuzzing-for-ble-logic-flaw-detection/

### Contribution
- A BLE fuzzing framework that uses an LLM as a semantic inference engine to interpret protocol intent and guide context-aware mutation.
- A specification-guided test generator that folds semantic constraints into field- and state-level mutations, producing dependency-consistent, state-aware test cases.
- On 19 real devices it found 34 previously unknown bugs, 9 of which received CVEs, with two recognized through a major vendor's bug bounty.

### Evaluation
- Across 9 SoC modules and 10 smartphones it found 36 security issues, with 9.34% higher code coverage than Proteus, previously the highest-coverage tool.
- LLM specification analysis reached up to 97% accuracy (packet dependencies) and response validation up to 85.8%; all 22 LL and 10 SMP message sequence charts were correctly turned into state machines.
- Because LLM response validation is around 85% accurate, some false positives and negatives remain in automated judgment, and final bugs need manual confirmation.

#### Comment
- Using an LLM to interpret specification text for protocol fuzzing is a practical direction that could apply to validating complex mobile wireless protocol implementations.
- Verification of Chinese institutions: a collaboration among several Chinese institutions (Xidian, Hainan, UCAS, Tsinghua) with Kanazawa University in Japan and Northern Arizona University in the US. Nine of the 34 bugs became CVEs, two were recognized through a vendor bounty as external validation, and the code is on GitHub with confirmed reproducibility, so the paper is included. Corresponding authors Yuqing Zhang (UCAS) and Qi Li (Tsinghua) are researchers with a verifiable security record.

---

# Better Safe than Sorry: Uncovering the Insecure Resource Management in App-in-App Cloud Services
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Super-apps such as WeChat, TikTok, Alipay, and Baidu give mini-app developers cloud databases, storage, and cloud functions, and hand them user identities. Checking that a user only touches their own resources, however, is left to the mini-app developer, and when that check is missing or wrong, attackers can read other users' data or skip payments. This paper is the first systematic study of the problem. Its tool, ICREMINER, combines static analysis with dynamic probing and found that 2,815 of 22,695 cloud-using mini-apps (12.40%) are affected, covering 8,062 insecure cloud operations.

Paper: https://www.ndss-symposium.org/ndss-paper/better-safe-than-sorry-uncovering-the-insecure-resource-management-in-app-in-app-cloud-services/

### Contribution
- Using platform documentation, it pinpoints where responsibility shifts from the super-app's identity management to the mini-app developer, and defines this as a new vulnerability class.
- It automates detection: client-side cloud operations are extracted statically, targets such as database names and file IDs are inferred, and actual accessibility is confirmed dynamically.
- It shows that mini-apps from large companies are affected, and it comes with responsible disclosure and mitigation advice.

### Evaluation
- From about 1.25 million mini-apps across four platforms, 22,695 that use cloud APIs were selected. Analysis took about 77 seconds per mini-app on average.
- Three experts reviewed the 3,057 flagged apps and 8,289 operations by consensus, and 97.26% of the operations were confirmed to expose sensitive resources. For 1,943 apps with read operations, unauthorized access was demonstrated using two test accounts.
- Write operations were not executed for ethical reasons; their impact (for example, payment bypass) was estimated through code semantics, so those damage figures are closer to estimates. Recall, meaning vulnerabilities the tool missed, was not measured.

#### Comment
- The paper is a useful reference for any mini-app ecosystem where the platform handles authentication but leaves authorization to developers.
- Most vulnerable apps are on WeChat (2,057), so the results depend heavily on one platform's ecosystem.
- Verification of a Chinese institution: the Fudan University systems security group (Min Yang, Zhemin Yang) is an established lab with a steady record at top venues in mobile and mini-app security. The manual validation and ethics procedures are described concretely, artifacts are on Zenodo, and the numbers do not look implausibly good, so the paper is included.

---

# Formal Analysis of BLE Secure Connection Pairing and Revelation of the PE Confusion Attack
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

BLE Secure Connection (SC) pairing is the latest protocol protecting sensitive data over BLE channels. Its complex flow, the difficulty of formalizing pairing-method selection, and overly idealized user assumptions had left it without a rigorous formal analysis. This paper analyzes BLE-SC pairing in Tamarin, modeling each participant's state machine and the pairing-method selection logic. Assuming stronger adversary capabilities, such as compromise of the temporary out-of-band channel, it verifies 84 pairing cases and in the process finds a new machine-in-the-middle attack, the PE confusion attack.

Paper: https://www.ndss-symposium.org/ndss-paper/formal-analysis-of-ble-secure-connection-pairing-and-revelation-of-the-pe-confusion-attack/

### Contribution
- The most detailed symbolic model of BLE-SC pairing to date, modeling host and controller as separate entities and formalizing the association-model selection logic.
- It reproduces the known method-confusion attack and uncovers the new PE confusion attack, with tools and proof-of-concept exploits for a controlled environment.
- For each of the 84 cases, defined by device capabilities and security requirements, it identifies the minimal security assumptions needed and proposes countermeasures.

### Evaluation
- Models were verified with the Tamarin Prover; because of time and compute limits, 16 representative cases were selected for distributed verification. Artifacts are on Zenodo and GitHub with a detailed reproduction procedure.
- Running only 16 of the 84 models as live experiments is a resource choice, justified by the identical generation and verification process across cases.
- Being formal-verification based, it reports only proof-of-concept figures rather than real success rates against commercial devices.

#### Comment
- It formally maps how BLE pairing security depends on the combination of user behavior and device capabilities, which is useful as a reference for wireless pairing security design.
- Verification of a Chinese institution: a collaboration between Wuhan University's information-security group (corresponding author Jing Chen) and Hong Kong Polytechnic University. The group has a steady security record, the formal model and PoC are on Zenodo and GitHub for verification, and a Tamarin-based proof is not the kind of result that can inflate performance numbers, so the paper is included.

---

# SIPConfusion: Exploiting SIP Semantic Ambiguities for Caller ID and SMS Spoofing
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

SIP is the signaling standard behind VoIP, VoLTE, and RCS messaging, and it includes authentication and identity-assertion mechanisms. Its flexibility, however, leaves room for servers and clients to interpret the same message differently, and those differences can lead to identity spoofing. The paper introduces SIPCHIMERA, a black-box fuzzing framework that systematically finds such ambiguity-based spoofing flaws. Across six open-source SIP servers and nine user agents, caller ID and SMS spoofing was possible in nearly every combination. The issues also affected real VoIP devices, commercial SIP services, and carrier-grade RCS platforms, and were disclosed to vendors.

Paper: https://www.ndss-symposium.org/ndss-paper/sipconfusion-exploiting-sip-semantic-ambiguities-for-caller-id-and-sms-spoofing/

### Contribution
- The first systematic study of SIP identity spoofing framed as interpretation mismatches between servers and clients rather than bugs in a single implementation.
- An automated method that derives test inputs from identity-related elements of the RFC grammars and compares them with the identity actually shown on the client.
- It shows that even where signature-based defenses such as STIR/SHAKEN are in place, interpretation gaps open new bypass paths, and proposes mitigations.

### Evaluation
- The testbed covers six servers (including Asterisk, OpenSIPS, and Kamailio) and nine clients (including Zoiper and Linphone), with both authenticated and unauthenticated attacker scenarios. Servers followed the security settings recommended in their official documentation.
- Real-world validation covered five VoIP devices, seven commercial SIP services, and three carrier-grade RCS messaging platforms.
- Results confirm whether vulnerabilities exist; how exploitable they are across commercial networks in general is limited to what was tested.

#### Comment
- Spoofed caller identity is where voice phishing and smishing begin, and this paper shows it remains possible at the protocol-interpretation level, making it important background for mobile research on call-based fraud.
- Verification of a Chinese institution: Haixin Duan's and Jianjun Chen's group at Tsinghua University has a consistent record at top venues on protocol ambiguity and web and network security. All test targets are public software, the tool is on GitHub, and responsible disclosure is documented, so the paper is included.

---

# Small Cell, Big Risk: A Security Assessment of 4G LTE Femtocells in the Wild
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Femtocells are small operator-deployed base stations placed in homes and offices to extend indoor coverage. Unlike ordinary base stations, they sit where attackers can physically reach the hardware, which creates new attack surface. This paper is the first systematic security evaluation of 4G LTE femtocells, combining analysis of commercial devices with Internet-wide measurement. Analyzing four commercial devices turned up five common vulnerabilities leading to local or remote compromise, and the measurement identified 86,108 suspected femtocell deployments. The authors confirmed in a real operator network that compromising a single femtocell gives an attacker a foothold against both the mobile core and subscribers.

Paper: https://www.ndss-symposium.org/ndss-paper/small-cell-big-risk-a-security-assessment-of-4g-lte-femtocells-in-the-wild/

### Contribution
- The first comprehensive security assessment of 4G femtocells, pairing commercial-device analysis with Internet-scale measurement.
- Experimental proof in a live operator network that a compromised femtocell is an entry point for attacks on both the core network and subscribers.
- Reported to GSMA and 3GPP SA3, which led 3GPP to approve a study item on strengthening 5G femtocell security and a work item for a Security Assurance Specification.

### Evaluation
- Clustering the measured devices put Korea Telecom first with 52,513 devices (60.99%); the devices span 103 countries, with South Korea first at 61.05%.
- Vulnerabilities were confirmed on real devices and the core-network attack was validated in a live network, but devices flagged as "suspected femtocells" in the measurement are inferred from banners and port features, so some may be misclassified.
- Ethics and the disclosure process are described in dedicated sections.

#### Comment
- Femtocells on Korean networks make up more than 60% of what was measured, so the findings bear directly on Korean mobile infrastructure security.
- Verification of a Chinese institution: led by Haixin Duan's group at Tsinghua University, with CableLabs and Carleton University, and with participation from the QI-ANXIN research institute. The group has a steady record at top networking-measurement venues, and the fact that the results fed into GSMA/3GPP standards work serves as external validation. The methodology and ethics are transparent, so the paper is included.
