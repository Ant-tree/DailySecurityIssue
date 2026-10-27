This file covers 7 peer-reviewed conference and journal papers in the Mobile category published in Q3 2026 (July to September). Preprints (arXiv, IACR ePrint) are excluded.

- Privacy (3)
- Other (4)

---

**Subcategory: Privacy**

# Bridges to Self: Silent Web-to-App Tracking on Mobile via Localhost
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

Browsers and mobile operating systems separate web and app contexts with sandboxing and process isolation, but this paper shows that on Android, Meta and Yandex actually broke that isolation to link web tracking with native identities. Using web standards such as HTTP(S), WebSocket, and WebRTC, they bridge mobile and web contexts over localhost, linking pseudonymous web cookies to long-lived native user IDs for persistent, stealthy cross-context tracking and deanonymization. The technique defeats cookie clearing, Incognito mode, advertising-ID resets, VPNs, and work/personal profile separation.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/vlummens

### Contribution
- Characterizes a previously undocumented web-to-app tracking paradigm over localhost using large-scale US and EU web crawls plus Android app analysis.
- Shows that Meta Pixel and Yandex Metrica started localhost bridging before accepting cookie consent banners.
- Evaluates browsers' post-disclosure patches and the Local Network Access (LNA) permission, and finds further bypass channels via global-unicast IPv6 in WebRTC and *.local mDNS lookups.

### Evaluation
- Combines large-scale web crawls from US and EU vantage points with systematic Android app analysis to measure channels that actually work.
- Includes a legal analysis and argues for revisiting platforms' and browsers' isolation principles, threat/trust models, protocol standards, and app review.
- Based on specific trackers' (Meta, Yandex) behavior at measurement time, which may have stopped or changed after disclosure.

#### Comment
- The point that web and app identities are linked over localhost on mobile is a highly important case from a mobile-security view of the tracking surface created by in-app WebViews and SDKs.
- Joint work by KU Leuven, IMDEA Networks Institute, and Radboud University, with an open PDF, published at USENIX Security.

---

# Health Hazard, Handle with Care: Investigating the Privacy Risks of Android's Health Connect
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

Android's Health Connect is a platform that mediates sharing of health and fitness data among apps. This paper analyzes the privacy risks by investigating how apps access health records they did not create and where that access diverges from the apps' Data Safety disclosures.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/spyridakis

### Contribution
- A systematic investigation of the privacy risks of cross-app health-data access through Health Connect.
- Reveals the discrepancy of apps accessing records created by other apps without disclosing it in their Data Safety section.

### Evaluation
- 28.49% of analyzed apps (100) accessed 2,334 records created by other apps, and 25 of them did not disclose that collection in Data Safety.
- 15.67% of apps accessed at least five records not their own, and 10% accessed at least 20. The grounds are concrete, based on real app measurement.

#### Comment
- By showing the gap between disclosure and actual access on a health-data mediation platform, it is a useful reference for mobile privacy and sensitive-data access control.
- Joint work by the Technical University of Crete, the University of Illinois Chicago, and the Cyprus University of Technology, published at USENIX Security.

---

# Plain Text, Plain Risks: Measuring HTTP Inclusion in Android WebViews at Scale
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

Widespread HTTPS and browser visual warnings have largely mitigated machine-in-the-middle attacks on the traditional web, but mobile is different: web content embedded via Android WebView has weaker protection. This paper compares WebView's handling of HTTP content with modern mobile browsers and measures HTTP inclusion at scale.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/beer

### Contribution
- Compares Android WebView's HTTP handling with mobile browsers, revealing several security shortcomings.
- Develops WebViewTrace, a static-dynamic analysis pipeline to systematically detect HTTP traffic and configurations in WebViews.
- The first large-scale empirical study of HTTP content in WebViews, across 189,779 apps.

### Evaluation
- Analyzing 189,779 apps, it quantifies a security-downgrade trend: 69.96% of apps that allow all HTTP traffic also relax the mixed-content policy.
- Case studies of popular apps show attack vectors from UI spoofing to full app takeover, and a qualitative study of 40 developers finds downgrades caused by misconceptions, compatibility needs, and third-party SDK demands.
- Strong grounds from combining large-scale measurement with a developer study.

#### Comment
- The attack surface created by WebView HTTP allowance and relaxed mixed-content policy is a direct reference for in-app WebView security and SDK-enforced configurations.
- Joint work by TU Wien and the University of Bayreuth, published at USENIX Security.

---

**Subcategory: Other**

# "Tap" Without Tapping: A Tag Discovery Forgery Attack on Android NFC
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

Tap-to-X apps such as tap-to-pay treat an NFC tag tap as proof of user proximity and intent. On Android, the OS reads tag data and dispatches it to the expected app, but the security of this post-discovery dispatch had been under-investigated. This paper identifies two OS-level design weaknesses that create a semantic origin gap, letting a local malicious app mimic a physical tap with no NFC interaction. The resulting tag-dispatch forgery attack (TDFA) affects real apps including Alipay, Huawei AI Life, and Samsung Galaxy Wearable.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/li-yilin

### Contribution
- Analyzes Android's post-tap tag dispatch and identifies two design weaknesses that allow forging a tap without a physical one.
- Proposes an OS-level fix and gives app-developer mitigations for use until it is available.

### Evaluation
- A large-scale analysis of 76,333 Google Play apps found 601 potentially affected apps with externally startable RW handlers, and on-device validation confirmed forged delivery in 498 of 597 installable, testable apps.
- Responsibly disclosed to the Android Security team, Alipay, and Huawei, who confirmed it; Google assigned CVE-2026-0081, and the authors received bug bounties.
- Strong grounds from combining large-scale measurement with on-device validation.

#### Comment
- Where an NFC tap serves as intent proof for payment and authentication, the finding that the OS dispatch design can be forged has direct implications for designing tap-based security flows.
- Verification of a Chinese institution: led by Shandong University with Simon Fraser University and City University of Hong Kong. External validation came through a CVE, vendor confirmation, and public artifacts (Zenodo), with concrete on-device results, so the paper is included.

---

# Cracks in the Walled Garden: Dissecting the Gray-Market of Unauthorized iOS App Distribution via Ad Hoc Sideloading
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

Apple enforces strict code signing and mandates distribution through the official App Store, yet the Ad Hoc provisioning mechanism, designed for developer testing, has become a channel for unauthorized app distribution. Using individual developer certificates and user-side signing to bypass app review, this practice has grown into a structured gray-market connecting certificate resale, third-party signing tools, and distribution of unsigned .ipa files. This paper is the first systematic study of that market, focused on its integrated service operations in China.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/liu-yijing

### Contribution
- The first systematic study of the gray-market for unauthorized iOS app distribution via Ad Hoc sideloading.
- Uncovers a multilayered certificate-circulation model with resale margins up to 3,000% and the common tricks signing tools use.
- Shows that most distributed apps are modified versions of legitimate ones using dynamic-library injection, which undermines app and system protections and exposes users to risk.

### Evaluation
- Through user-centric collection, it identified 3,359 active signing sites for certificate redemption, reverse-engineered 12 signing tools, and obtained 8,216 distributed .ipa entries.
- Broad real-market data gives concrete grounds, with the China-centered scope stated explicitly.

#### Comment
- It tackles iOS code signing, dynamic-library injection, and app tampering head-on, making it a very direct case for designing iOS security SDKs and integrity/runtime protection, closely tied to the user's interest in iOS binary protection.
- Verification of a Chinese institution: from Tsinghua University and BNRist (Baojun Liu, Haixin Duan, and others), a group with a steady top-tier record in network and ecosystem measurement. Public artifacts (Zenodo) and a concrete collection method make it reproducible, so it is included. Published at USENIX Security.

---

# Raising the Flag: Detecting Missing Permission Controls in Mini-Program APIs
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

Super-app mini-programs are given APIs that reach OS-like sensitive capabilities. This paper addresses detecting where permission controls are missing in mini-program APIs: it finds which APIs should go through a permission check but do not, exposing flaws that can lead to unauthorized access.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/wei-zhiao

### Contribution
- A method to detect missing permission controls in mini-program APIs, systematically finding API-level authorization flaws in the capabilities super-app platforms provide.
- Derives candidate flaws by comparing which APIs should have a permission check with whether one is actually performed.

### Evaluation
- (The full text was retrieved, but the summary digest did not surface enough detailed figures. The evaluation consists of analyzing the set of mini-program APIs and validating the flaws found.)
- Grounded in analysis of real platform APIs; detailed figures are best confirmed against the original.

#### Comment
- It addresses flaws in the pattern where a super-app provides authentication but leaves authorization to API implementations, and together with Q1's app-in-app cloud-resource study (NDSS 2026) it shows a recurring theme in mini-program ecosystem security.
- Joint work by the University of Waterloo, The Ohio State University, and the University of Illinois Urbana-Champaign, published at USENIX Security.

---

# SoK: History Doesn't Repeat Itself, but Android Design-Level Vulnerabilities Rhyme in OpenHarmony
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

This systematization-of-knowledge paper examines how long-known design-level vulnerabilities in Android recur in similar forms in OpenHarmony, an emerging mobile OS. By comparing the two systems' designs, it shows that the same categories of design flaws reappear even as the platform changes.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/chen-hongkai

### Contribution
- Systematizes categories of Android design-level vulnerabilities and maps them onto OpenHarmony to analyze how they recur in an emerging OS.
- Distills the common causes of design flaws that repeat across platforms, offering lessons for defensive design.

### Evaluation
- A systematization comparing Android and OpenHarmony designs, benchmarking the two platforms against known vulnerability categories.
- Focuses on classifying design flaws and their recurrence rather than on measured success rates of new attacks.

#### Comment
- As OpenHarmony spreads, it shows how far Android's design lessons carry over, making it a useful reference for designing multi-platform mobile security SDKs. It is filed under "Other" as it fits no specific subcategory.
- Joint work by Arizona State University, CISPA, and The Ohio State University, published at USENIX Security.
