# Literature Review: AR Spatial Anchoring Techniques

## Paper Configuration Record

| Parameter | Value |
|-----------|-------|
| **Topic** | AR spatial anchoring techniques |
| **Paper Type** | Literature Review |
| **Discipline** | Computer Science / Human-Computer Interaction (Augmented Reality, SLAM) |
| **Citation Format** | IEEE |
| **Output Format** | Markdown |
| **Body Language** | English (with zh-TW section summaries) |
| **Domain Evidence Profile** | `cs_ml` — admits arXiv preprints and conference proceedings alongside peer-reviewed journal articles |
| **Operational Mode** | `lit-review` |

### Notes
Search was conducted via general web search cross-referencing arXiv, PubMed Central, MDPI *Sensors*, ACM Digital Library abstracts, and primary vendor technical documentation (Google ARCore). This is **not** a formal multi-database Boolean search executed directly against IEEE Xplore / Scopus / ACM DL APIs — no such direct database access was available in this session. Coverage should be treated as a bounded, single-pass web-search sweep (last searched: 2026-09-09), not an exhaustive systematic review. This limitation is disclosed per the search-bounded novelty convention rather than implying global completeness.

---

## Literature Search Report

### Search Strategy
- **Concepts**: (spatial anchor OR world anchor OR persistent anchor) AND (augmented reality OR mixed reality) AND (SLAM OR localization OR tracking OR registration)
- **Secondary concepts**: cloud anchors, marker-based/markerless registration, collaborative/multi-user localization, outdoor geo-anchoring, semantic anchoring, cross-platform interoperability (WebXR)
- **Sources searched**: arXiv (cs.CV / cs.RO / cs.HC / cs.GR), PubMed Central, MDPI *Sensors*, ACM Digital Library (abstracts), IEEE Xplore (abstracts via secondary indexing), Google Developer documentation (ARCore)
- **Date range**: 1997 (foundational) + 2020–2025 (current techniques); no explicit exclusion of older foundational work
- **Language**: English
- **Last searched**: 2026-09-09

### Coverage Distribution Advisory

`DISTRIBUTIONAL_SKEW_ADVISORY`:
- **Dimension**: time distribution
- **Concentration**: 2020s = 9/10 (90%) of dated sources (excluding the 1997 foundational survey, included deliberately for conceptual lineage)
- **Advisory**: This is expected given AR spatial anchoring's recent technical maturation (cloud-anchor APIs, transformer-based geo-localization, LLM-driven placement all post-2020) rather than a defect in search execution. A historical-lineage reader should note the corpus is weighted toward the current state of the art.
- **Search response**: no expansion — the recency concentration substantively reflects the field's development timeline; the Azuma (1997) foundational work is retained to anchor terminology and the registration/tracking framing that later work builds on.

No other dimension (geographic, methodological, venue tier) reached the 70% threshold: sources span journal (*Sensors*, *IEEE Trans. Robotics*, *Presence*), conference (IEEE VR, ISMAR, UIST), and preprint (arXiv, undergoing or pending peer review) venues, and cover SLAM-engineering, HCI/user-study, and systems/standards methodologies.

### Screening Results
- Initial web-search hits across 8 targeted queries: ~70 results
- After title/abstract screening: 22 candidates
- After full-text (abstract + summary) assessment: 11 sources included
- Excluded: marketing/statistics reports (AR market-adoption studies), patent filings without peer review, and blog/tutorial content not carrying independent technical claims beyond what the primary vendor documentation already states

### Annotated Bibliography

#### Azuma, R. T. (1997). A Survey of Augmented Reality.
- **Type**: Journal article (*Presence: Teleoperators and Virtual Environments*)
- **Method**: Narrative survey / taxonomy
- **Key Findings**: Establishes the definition of AR (combines real and virtual, real-time interactive, 3-D registered) and identifies registration and sensing error as the field's two central unsolved problems.
- **Relevance**: Provides the conceptual and terminological lineage for "registration," which spatial anchoring is the modern instantiation of.
- **Quality**: Foundational, extremely widely cited; pre-dates modern SLAM-based anchoring but frames the problem class accurately.
- **Potential Use**: Introduction (problem framing, terminology).

#### Campos, C., Elvira, R., Gómez Rodríguez, J. J., Montiel, J. M. M., & Tardós, J. D. (2021). ORB-SLAM3: An Accurate Open-Source Library for Visual, Visual–Inertial, and Multimap SLAM.
- **Type**: Journal article (*IEEE Transactions on Robotics*, 37(6))
- **Method**: Feature-based visual/visual-inertial SLAM, MAP estimation, multi-map place recognition
- **Key Findings**: Achieves 2–10x accuracy improvement over prior SLAM systems; introduces multi-map merging so tracking loss does not discard prior maps, a mechanism directly relevant to anchor re-localization after tracking failure.
- **Relevance**: Represents the SLAM substrate that most feature-point-based spatial anchors (including cloud anchors) are built on.
- **Quality**: High — open-source, benchmarked, peer-reviewed, widely adopted as an SLAM baseline.
- **Potential Use**: Theme 1 (SLAM-based anchor construction).

#### Sadeghi-Niaraki, A., & Choi, S.-M. (2020). A Survey of Marker-Less Tracking and Registration Techniques for Health & Environmental Applications to Augmented Reality and Ubiquitous Geospatial Information Systems.
- **Type**: Journal article (*Sensors*, 20(10))
- **Method**: Narrative survey / taxonomy (sensor-based vs. vision-based tracking)
- **Key Findings**: Organizes markerless techniques into sensor-based (inertial, acoustic, magnetic) and vision-based (feature/edge/template matching, optical flow, depth, SLAM) categories; concludes hybrid approaches are necessary for complex real-world applications.
- **Relevance**: Provides the taxonomic backbone for comparing anchoring approaches by sensing modality.
- **Quality**: Peer-reviewed, systematic, though domain-scoped to health/geospatial applications rather than AR generally.
- **Potential Use**: Theme 2 (marker-based vs. markerless registration).

#### Israr, S., Khan, D., Cheng, Z., Khan, M., & Kiyokawa, K. (2025). GHAR: GeoPose-based Handheld Augmented Reality for Architectural Positioning, Manipulation and Visual Exploration. arXiv:2506.14414.
- **Type**: Preprint (arXiv, cs.GR)
- **Method**: Markerless GeoPose-based 7-DOF tracking, gesture-based manipulation
- **Key Findings**: User studies show significant usability, manipulability, and comprehensibility gains over marker-based alternatives for architectural visualization.
- **Relevance**: Direct empirical marker-vs-markerless comparison in a spatial-anchoring application context (construction/architecture).
- **Quality**: Preprint (admitted under `cs_ml` profile) — includes a user study, not yet confirmed peer-reviewed at time of writing.
- **Potential Use**: Theme 2; Discussion (application-specific evidence).

#### Google Developers. Cloud Anchors — ARCore. (Technical documentation, accessed 2026-09-09.)
- **Type**: Primary vendor technical documentation
- **Method**: N/A (platform/API description)
- **Key Findings**: Documents the cloud-anchor architecture — hosting an anchor uploads its SLAM feature-point data to a cloud endpoint under a unique ID; resolving on another device recreates the shared coordinate frame; ARCore centralizes maps in the cloud while ARKit historically used peer-to-peer `ARWorldMap` sharing.
- **Relevance**: Canonical description of the dominant industry implementation pattern for persistent, shareable spatial anchors.
- **Quality**: Authoritative for platform behavior, but non-peer-reviewed and vendor-authored (no independent accuracy benchmarking).
- **Potential Use**: Theme 1 (persistence); Theme 3 (cross-platform sharing architecture).

#### Miller, J., Soltanaghai, E., Duvall, R., Chen, J., Bhat, V., Pereira, N., & Rowe, A. (2021). Multi-User Augmented Reality with Infrastructure-free Collaborative Localization. arXiv:2111.00174.
- **Type**: Preprint (arXiv)
- **Method**: Visual-inertial odometry fused with UWB ranging via collaborative particle filtering
- **Key Findings**: Median 3D localization error under 1 m across five users on three floors, without fixed infrastructure or a shared pre-built map.
- **Relevance**: Alternative to cloud-anchor-based multi-user sharing — establishes a common reference frame via peer ranging rather than shared visual maps.
- **Quality**: Preprint, empirically validated across a real multi-floor deployment; not yet confirmed as peer-reviewed venue publication.
- **Potential Use**: Theme 3 (collaborative/multi-user anchoring, infrastructure-free alternative).

#### Mithun, N. C., Minhas, K., Chiu, H.-P., Oskiper, T., Sizintsev, M., Samarasekera, S., & Kumar, R. (2023). Cross-View Visual Geo-Localization for Outdoor Augmented Reality. IEEE VR 2023.
- **Type**: Conference paper (IEEE VR)
- **Method**: Transformer-based network with triplet ranking loss, matching ground-level imagery to aerial/satellite imagery for location + orientation estimation; extended with temporal video fusion
- **Key Findings**: State-of-the-art results on geo-localization benchmarks; achieves stable, high-precision AR content insertion outdoors without relying on GPS alone.
- **Relevance**: Addresses the outdoor anchoring problem where GPS accuracy and SLAM feature persistence both degrade.
- **Quality**: Peer-reviewed conference publication with benchmark evaluation.
- **Potential Use**: Theme 4 (outdoor/geospatial anchoring).

#### Navard, P., & Yilmaz, A. (2024). A Probabilistic-based Drift Correction Module for Visual Inertial SLAMs. arXiv:2404.10140.
- **Type**: Preprint (arXiv, cs.RO)
- **Method**: Probabilistic modular correction — models positioning as a multivariate random variable, finds the mode maximizing likelihood under geometric motion priors
- **Key Findings**: Reports approximately 10x reduction in drift error over extended traversals; designed to be integrated into existing SLAM/VIO pipelines rather than replacing them.
- **Relevance**: Drift is the primary threat to long-duration anchor stability; this offers a plug-in mitigation.
- **Quality**: Preprint; reported gains are from the authors' own benchmarks and not yet independently replicated in the literature reviewed here.
- **Potential Use**: Theme 4 (drift correction as an anchoring-stability mechanism).

#### Yoffe, L., Sharma, A., & Höllerer, T. (2023). OCTOPUS: Open-vocabulary Content Tracking and Object Placement Using Semantic Understanding in Mixed Reality. IEEE ISMAR 2023.
- **Type**: Conference paper (IEEE ISMAR)
- **Method**: 8-stage pipeline combining segmentation models, vision-language models, and LLM reasoning for open-vocabulary object placement
- **Key Findings**: Matches human-expert placement judgments in ~57% of cases in a preliminary user study; generalizes across object categories without fine-tuning.
- **Relevance**: Represents a shift from purely geometric (SLAM feature-point) anchoring toward semantic anchoring — placing content relative to recognized real-world entities rather than raw geometry.
- **Quality**: Peer-reviewed (ISMAR is the primary AR/MR venue); the 57% figure indicates the approach is promising but not yet reliable enough to fully replace human placement judgment.
- **Potential Use**: Theme 5 (semantic/content-aware anchoring).

#### Numan, N., Van Brummelen, J., Lu, Z., & Steed, A. (2025). AdjustAR: AI-Driven In-Situ Adjustment of Site-Specific Augmented Reality Content. ACM UIST 2025 (Poster).
- **Type**: Conference poster (ACM UIST)
- **Method**: Multimodal LLM compares authored vs. live camera views to detect environmental drift and re-project corrected 2D placements into 3D
- **Key Findings**: Demonstrates automatic re-alignment of AR content as the physical environment changes over time (furniture moved, renovation, seasonal change), addressing a failure mode that purely geometric anchors cannot self-correct.
- **Relevance**: Directly targets long-term anchor validity under environmental change — a gap identified below.
- **Quality**: Poster-stage publication (early-stage, not a full peer-reviewed paper); placement heuristic is currently limited to a bottom-center anchoring strategy per the authors' own stated future work.
- **Potential Use**: Theme 5; Research Gaps (longitudinal anchor validity).

#### Macario, G. (2024). WebXR, A-Frame and Networked-Aframe as a Basis for an Open Metaverse: A Conceptual Architecture. arXiv:2404.05317.
- **Type**: Preprint (arXiv)
- **Method**: Conceptual/architectural proposal built on WebXR, A-Frame, Networked-Aframe
- **Key Findings**: Proposes a web-standards-based architecture for cross-platform, interoperable spatial experiences, positioning WebXR's anchors module as a path toward vendor-neutral anchor interoperability.
- **Relevance**: Frames the standards-layer alternative to proprietary cloud-anchor ecosystems (ARCore/ARKit/Azure Spatial Anchors).
- **Quality**: Preprint, conceptual/architectural rather than empirically evaluated.
- **Potential Use**: Theme 6 (interoperability and standards); Research Gaps.

### Literature Matrix

| Source | SLAM/Persistence | Marker vs. Markerless | Collaborative/Multi-user | Outdoor/Geo | Semantic Anchoring | Standards/Interop | Method | Quality |
|--------|:---:|:---:|:---:|:---:|:---:|:---:|--------|---------|
| Azuma (1997) | x | main | | | | | Survey | High (foundational) |
| Campos et al. (2021) | main | | | | | | SLAM/systems | High |
| Sadeghi-Niaraki & Choi (2020) | x | main | | | | | Survey | High |
| Israr et al. (2025) | | main | | | | | Quant + user study | Medium (preprint) |
| Google ARCore docs | main | | x | | | x | Technical doc | Medium (vendor) |
| Miller et al. (2021) | x | | main | | | | Quant (field study) | Medium (preprint) |
| Mithun et al. (2023) | | | | main | | | Quant (benchmark) | High |
| Navard & Yilmaz (2024) | main | | | x | | | Quant (algorithmic) | Medium (preprint) |
| Yoffe et al. (2023) | | | | | main | | Mixed (system + user study) | High |
| Numan et al. (2025) | | | | | main | | Mixed (system + demo) | Medium (poster) |
| Macario (2024) | | | | | | main | Conceptual/architecture | Medium (preprint) |

### Identified Gaps

1. **Longitudinal anchor validity.** Almost all included work evaluates anchoring accuracy at or near creation time; only AdjustAR [10] addresses re-alignment after the physical environment changes, and its placement heuristic is still limited (bottom-center only). Systematic longitudinal studies of anchor drift/invalidation over weeks or months are absent from this corpus.
2. **Cross-platform standardization is architecturally proposed but not empirically validated.** Macario [11] describes a WebXR-based interoperability path, but no source in this corpus reports a head-to-head accuracy/latency comparison between a standards-based (WebXR anchors module) and a proprietary (ARCore/ARKit cloud anchor) implementation.
3. **Semantic anchoring reliability ceiling.** OCTOPUS [9] matches human placement judgment only ~57% of the time; no included source benchmarks semantic-anchoring approaches against each other or establishes what accuracy threshold is acceptable for production use.
4. **Outdoor large-scale evaluation at anchor density.** Mithun et al. [7] and Navard & Yilmaz [8] address geo-localization and drift individually, but no source evaluates anchor accuracy under high spatial anchor density outdoors (e.g., city-scale AR navigation with many co-located persistent anchors).
5. **Collaborative anchoring beyond small groups.** Miller et al.'s infrastructure-free approach [6] is validated with five users; multi-user cloud-anchor sharing patterns are described in vendor documentation [5] but without published accuracy/scalability data for larger concurrent user counts.

### Recommended Sources by Section

| Section | Key Sources |
|---------|------------|
| Introduction | Azuma [1], Sadeghi-Niaraki & Choi [3] |
| SLAM-Based Anchor Construction | Campos et al. [2], Google ARCore [5] |
| Marker vs. Markerless Registration | Sadeghi-Niaraki & Choi [3], Israr et al. [4] |
| Collaborative/Multi-user Anchoring | Google ARCore [5], Miller et al. [6] |
| Outdoor/Geospatial Anchoring | Mithun et al. [7], Navard & Yilmaz [8] |
| Semantic Anchoring | Yoffe et al. [9], Numan et al. [10] |
| Standards/Interoperability | Macario [11] |
| Research Gaps / Future Work | Numan et al. [10], Macario [11] |

---

## Literature Review

### 1. Introduction

Augmented reality (AR) systems must solve a persistent registration problem: virtual content has to be positioned and re-positioned correctly relative to the physical world across time, devices, and users. Azuma's foundational survey framed this as the field's central open problem two decades before "spatial anchor" became the standard industry term [1]. A spatial anchor, in current usage, is a fixed reference frame — typically a cluster of visual feature points or surface geometry captured during simultaneous localization and mapping (SLAM) — that lets an AR system recall and reproduce a real-world pose across sessions, devices, or users [3]. This review synthesizes recent literature (2020–2025), supplemented by foundational SLAM and AR-survey work, across six themes: SLAM-based anchor construction, marker-based versus markerless registration, collaborative/multi-user anchoring, outdoor/geospatial anchoring, semantic anchoring, and cross-platform standards.

> **摘要（繁體中文）**：擴增實境（AR）的核心挑戰在於如何讓虛擬內容在時間、裝置與使用者之間保持正確的空間對位。「空間錨點」是目前業界用以描述此對位機制的標準術語，其本質是透過 SLAM 擷取的視覺特徵點或表面幾何資訊所建立的參考座標系。本文回顧 2020–2025 年間六大主題的相關文獻：SLAM 錨點建構、有標記與無標記註冊技術、多使用者協作式錨定、戶外地理空間錨定、語意錨定，以及跨平台標準化。

### 2. SLAM-Based Anchor Construction and Persistence

Modern spatial anchors are built on top of visual or visual-inertial SLAM. ORB-SLAM3 [2] exemplifies the current state of the art: it fuses monocular, stereo, or RGB-D input with inertial measurement, and — critically for anchoring — introduces multi-map place recognition, so that a device which loses tracking starts a new local map that is later merged with earlier maps upon revisiting the same physical area. This directly addresses one of anchoring's core failure modes: tracking loss invalidating a previously established anchor.

Industry cloud-anchor systems build persistence and sharing on top of this SLAM substrate. ARCore's Cloud Anchors work by uploading a device's local feature-point cloud around a declared anchor point to a cloud endpoint, returning a unique ID that another device can later use to resolve — i.e., re-localize against — the same physical point [5]. ARKit historically achieved a similar effect through peer-to-peer `ARWorldMap` sharing rather than centralized cloud storage [5]. This architectural difference (centralized vs. peer-to-peer map sharing) recurs as a theme in the collaborative-anchoring literature below.

> **重點摘要（繁體中文）**：現代空間錨點建立於視覺或視覺慣性 SLAM 之上。ORB-SLAM3 引入多地圖辨識機制，可在追蹤中斷後無縫合併地圖，直接改善錨點失效的問題；而 ARCore 的雲端錨點則是將特徵點雲上傳至雲端以供其他裝置重新定位，ARKit 則採用點對點地圖共享架構。

### 3. Marker-Based versus Markerless Registration

Sadeghi-Niaraki and Choi's survey organizes markerless registration into sensor-based (inertial, acoustic, magnetic) and vision-based (feature matching, template matching, optical flow, depth imaging, SLAM) categories, concluding that hybrid combinations are typically necessary for robust real-world performance [3]. This taxonomy remains a useful lens for classifying anchoring techniques by their underlying sensing modality rather than by application domain alone.

Empirical comparisons continue to favor markerless approaches for usability at the cost of some setup complexity. Israr et al.'s GHAR system uses GeoPose-based markerless tracking to give handheld AR content full 7-DOF manipulation (3-DOF translation, 3-DOF rotation, 1-DOF scale) for architectural visualization, and reports significant usability and comprehensibility improvements over marker-dependent alternatives in user studies [4]. This is consistent with the general industry trend away from fiducial markers, though marker-based approaches retain advantages in constrained, high-precision contexts (e.g., surgical registration) that fall outside this review's AR-anchoring scope.

> **重點摘要（繁體中文）**：無標記式追蹤技術可分為感測器式與視覺式兩大類，混合式方法通常能提供更穩健的效能。GHAR 系統採用 GeoPose 無標記追蹤，在建築視覺化的使用者研究中展現優於有標記方案的可用性與理解度。

### 4. Collaborative and Multi-User Spatial Anchoring

Sharing a spatial anchor across users establishes a common coordinate frame that lets multiple people perceive co-located virtual content consistently [5]. The dominant industry pattern relies on shared SLAM maps — either centralized (ARCore's cloud anchors) or peer-to-peer (ARKit's `ARWorldMap` sharing) [5]. An alternative, infrastructure-free approach is demonstrated by Miller et al., who fuse visual-inertial odometry with ultra-wideband ranging through a collaborative particle filter, achieving sub-meter median localization error across five users on three floors without any shared pre-built map or fixed infrastructure [6]. This suggests that map-sharing is not strictly necessary for multi-user spatial agreement when peer-to-peer ranging hardware is available, trading map-based semantic richness for infrastructure independence.

> **重點摘要（繁體中文）**：多使用者共享空間錨點的主流做法依賴共享 SLAM 地圖（集中式或點對點）。Miller 等人提出免基礎設施的協作方法，結合視覺慣性里程計與超寬頻測距，在無需共享地圖的情況下達成次公尺級定位誤差，顯示地圖共享並非多使用者空間一致性的必要條件。

### 5. Outdoor and Geospatial Anchoring

Outdoor AR anchoring faces two compounding problems: GPS alone lacks the precision for stable content placement, and SLAM feature persistence degrades under lighting/seasonal change and large-scale drift. Mithun et al. address the first by matching ground-level camera views against aerial/satellite imagery using a transformer-based network with a triplet ranking loss, estimating both location and orientation and achieving stable high-precision AR insertion outdoors [7]. Navard and Yilmaz address the second directly: their probabilistic drift-correction module models positioning as a multivariate random variable and reports roughly a 10x reduction in accumulated drift over extended traversals, while being designed as a modular add-on to existing SLAM/VIO pipelines rather than a replacement system [8]. Together these represent complementary strategies — external geo-referencing and internal drift modeling — for the outdoor anchoring problem.

> **重點摘要（繁體中文）**：戶外錨定面臨 GPS 精度不足與 SLAM 長時間漂移兩大挑戰。Mithun 等人利用空拍影像進行地理定位比對以提升精度；Navard 與 Yilmaz 則提出可模組化整合的機率式漂移修正方法，兩者分別從外部地理參考與內部漂移建模互補解決此問題。

### 6. Semantic Anchoring and Standards Interoperability

A more recent direction anchors content to recognized real-world *entities* rather than raw geometric feature points. Yoffe et al.'s OCTOPUS pipeline combines segmentation, vision-language models, and LLM reasoning to place open-vocabulary virtual objects into a scene without per-object fine-tuning, matching human expert placement judgment in roughly 57% of cases in a preliminary study [9] — promising, but not yet reliable enough to fully automate. Numan et al.'s AdjustAR extends this idea temporally: a multimodal LLM compares an originally authored view against the current live camera feed to detect environmental drift and automatically re-project corrected placements, directly targeting the problem of anchors becoming invalid as the physical world changes [10]. Both systems currently rely on relatively simple placement heuristics (e.g., AdjustAR's bottom-center strategy) that the original authors flag as an area for future refinement.

At the infrastructure level, cross-platform interoperability remains largely unresolved. Macario proposes a WebXR/A-Frame/Networked-Aframe architecture as a path toward a vendor-neutral, web-standards-based alternative to the proprietary cloud-anchor ecosystems described above [11], positioning the WebXR Anchors Module as the interoperability layer that could, in principle, let anchors created on one platform resolve correctly on another — a capability current proprietary systems do not generally provide.

> **重點摘要（繁體中文）**：語意錨定將內容錨定於可辨識的真實世界實體，而非單純幾何特徵點。OCTOPUS 利用視覺語言模型與大型語言模型進行開放詞彙物件放置，準確率約 57%；AdjustAR 則進一步處理環境隨時間改變後的錨點失準問題。在跨平台互通性方面，WebXR 架構被提出作為取代專屬雲端錨點生態系的標準化路徑，但目前仍缺乏實證評估。

### 7. Cross-Cutting Synthesis

**Convergent findings.** Across all six themes, persistence and drift are the recurring failure modes that every approach must address in some form — whether through SLAM map merging [2], modular drift correction [8], infrastructure-free re-ranging [6], or LLM-driven re-alignment [10]. There is also a clear directional convergence away from purely geometric anchoring toward semantically- or context-aware anchoring [9], [10], mirroring the broader trend of vision-language models entering spatial computing pipelines.

**Divergent findings and debates.** The literature does not converge on a single architecture for multi-user sharing: centralized cloud maps [5], peer-to-peer map sharing [5], and infrastructure-free ranging [6] each solve the same problem with different infrastructure and privacy trade-offs, and no source in this corpus directly compares them head-to-head. Similarly, whether markerless approaches should fully replace marker-based ones remains context-dependent rather than settled [3], [4].

**Methodological observations.** Quantitative SLAM/algorithmic benchmarking dominates the SLAM-persistence and outdoor/geo themes [2], [7], [8], while the semantic-anchoring theme relies more on small-scale user studies and preliminary evaluations [9], [10] — reflecting the relative immaturity of LLM-driven placement compared to geometric SLAM. Standards/interoperability work in this corpus is architectural/conceptual rather than empirical [11].

### 8. Research Gaps and Future Directions (recap)

See "Identified Gaps" above. In brief: longitudinal anchor validity under environmental change, empirical (not just architectural) cross-platform interoperability evaluation, reliability benchmarking for semantic anchoring, outdoor evaluation at realistic anchor density, and multi-user anchoring evaluation beyond small groups are the most actionable openings for future work.

### 9. Conclusion

Spatial anchoring has moved from Azuma's 1997 framing of "registration" as an unsolved general problem [1] to a maturing but still fragmented set of techniques: SLAM-based persistence and multi-map recovery [2], marker/markerless registration [3], [4], multiple competing multi-user sharing architectures [5], [6], complementary outdoor drift/geo-localization strategies [7], [8], early-stage semantic and temporally-adaptive anchoring [9], [10], and an as-yet-unproven standards path toward cross-platform interoperability [11]. The field's current center of gravity is shifting from "can we place content accurately once" toward "can that placement remain valid, sharable, and semantically sensible over time and across platforms" — the open questions catalogued above.

---

## AI Disclosure

This literature review was produced with AI assistance (Claude, Anthropic) using the `academic-paper` skill's `lit-review` mode. Source discovery was performed via web search rather than direct database API access (see Search Strategy note above on this bound); every source's title, authorship, and venue was independently verified via the publisher/preprint page before inclusion, per the pipeline's citation-fabrication prohibition. No citation in this document was generated from model memory alone. The synthesis, thematic organization, and gap analysis reflect AI-assisted drafting and should be reviewed by a domain expert before use in a submitted manuscript.

---

## References (IEEE)

[1] R. T. Azuma, "A survey of augmented reality," *Presence: Teleoperators and Virtual Environments*, vol. 6, no. 4, pp. 355–385, 1997.

[2] C. Campos, R. Elvira, J. J. Gómez Rodríguez, J. M. M. Montiel, and J. D. Tardós, "ORB-SLAM3: An accurate open-source library for visual, visual–inertial, and multimap SLAM," *IEEE Trans. Robotics*, vol. 37, no. 6, pp. 1874–1890, Dec. 2021.

[3] A. Sadeghi-Niaraki and S.-M. Choi, "A survey of marker-less tracking and registration techniques for health & environmental applications to augmented reality and ubiquitous geospatial information systems," *Sensors*, vol. 20, no. 10, 2020.

[4] S. Israr, D. Khan, Z. Cheng, M. Khan, and K. Kiyokawa, "GHAR: GeoPose-based handheld augmented reality for architectural positioning, manipulation and visual exploration," arXiv:2506.14414, 2025.

[5] Google Developers, "Cloud Anchors — ARCore," Google for Developers, accessed Sep. 9, 2026. [Online]. Available: https://developers.google.com/ar/develop/cloud-anchors

[6] J. Miller, E. Soltanaghai, R. Duvall, J. Chen, V. Bhat, N. Pereira, and A. Rowe, "Multi-user augmented reality with infrastructure-free collaborative localization," arXiv:2111.00174, 2021.

[7] N. C. Mithun, K. Minhas, H.-P. Chiu, T. Oskiper, M. Sizintsev, S. Samarasekera, and R. Kumar, "Cross-view visual geo-localization for outdoor augmented reality," in *Proc. IEEE Conf. Virtual Reality and 3D User Interfaces (VR)*, 2023.

[8] P. Navard and A. Yilmaz, "A probabilistic-based drift correction module for visual inertial SLAMs," arXiv:2404.10140, 2024.

[9] L. Yoffe, A. Sharma, and T. Höllerer, "OCTOPUS: Open-vocabulary content tracking and object placement using semantic understanding in mixed reality," in *Proc. IEEE Int. Symp. Mixed and Augmented Reality (ISMAR)*, 2023.

[10] N. Numan, J. Van Brummelen, Z. Lu, and A. Steed, "AdjustAR: AI-driven in-situ adjustment of site-specific augmented reality content," in *Adjunct Proc. ACM Symp. User Interface Software and Technology (UIST)*, 2025.

[11] G. Macario, "WebXR, A-Frame and Networked-Aframe as a basis for an open metaverse: A conceptual architecture," arXiv:2404.05317, 2024.
