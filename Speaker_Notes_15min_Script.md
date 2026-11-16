# IS5542 Final Group Project — 15-Minute Presentation Script & Speaker Notes
**Project Title**: ClaimGuard AI — Multimodal Agentic Workflow for HK Insurance Claims & Fraud Triage  
**Total Time**: 15 Minutes (Strictly aligned with `IS5542 Project Template.pptx` allocation: 2m + 7m + 4m + 2m)  
**Data Integrity Standard**: Grounded in public statistics from the **HK Insurance Authority (IA 2024)**, **HK Federation of Insurers (HKFI 2024–2025)**, **ICAC / HK Police enforcement cases**, and **Allianz / AXA / Zurich** published benchmarks, paired with an illustrative mid-sized HK insurer ROI model and 3 simulated prototype scenarios.

---

## Slide 1: Title Slide (0:00 – 0:30 | Presenter 1)
### English Verbatim Script
> "Good afternoon Professor and classmates. Today, our team is proud to present **ClaimGuard AI**—a defensible, multimodal agentic workflow designed for Hong Kong medical and auto insurance claims triage. Grounded in real regulatory data from the Hong Kong Insurance Authority and global insurer benchmarks like Allianz and AXA, we will walk you through the business problem, our hybrid three-model architecture, a live working prototype, and an illustrative ROI model."

---

## Slide 2: Agenda & Team Workflow (0:30 – 0:50 | Presenter 1)
### English Verbatim Script
> "Our 15-minute presentation covers four core modules: first, the real market pressure and fraud challenges in Hong Kong insurance; second, our four-stage deterministic harness and live prototype walkthrough; third, real-world insurer benchmarks and our illustrative financial ROI model; and finally, ongoing governance under NIST AI RMF and HK IA Guideline 10."

---

## Part 1: Business Problem (Total: 2 Minutes | 0:50 – 2:50)

### Slide 3: HK Claims Inflation & Fraud Leakage (0:50 – 1:50 | Presenter 1)
#### Real-World Facts Cited
* **IA 2024 Full-Year Statistics**: HK General Insurance paid **HK$53.0 billion** in gross claims (**HK$28.1 billion** direct); **Accident & Health** is the largest direct segment (**HK$22.8 billion** gross premiums). Long-term claims/benefits reached **HK$352.5 billion**.
* **HKFI 2024–2025 Medical Inflation**: Reached **10.3%** in 2024 (vs. 1.7% general inflation); HKFI formally warned the Health Bureau about **Fraud, Wastage, and Abuse (FWA)**.
* **ICAC & HK Police Real Cases**: Convictions involving bogus medical receipts and sick notes submitted to insurers like AIA, "crash-for-cash" rings, and multi-policy scams up to **HK$37.5 million**.

#### English Verbatim Script
> "Let's ground our business problem in official Hong Kong market data. According to the **Hong Kong Insurance Authority (IA)**, Hong Kong's general insurance sector paid **53 billion HKD** in gross claims in 2024, with **Accident and Health** standing as the largest direct insurance line. Meanwhile, the **Hong Kong Federation of Insurers (HKFI)** reported that medical inflation surged to **10.3%** in 2024—more than six times general inflation—and formally flagged **Fraud, Wastage, and Abuse** as a structural driver of claims leakage.
> This isn't theoretical: **ICAC** and Hong Kong Police enforcement records show recurring convictions for fake medical receipts, forged sick leave certificates submitted to insurers like AIA, and syndicated multi-policy scams reaching up to **37.5 million HKD**. Yet frontline claims adjusters still manually cross-check messy bilingual handwritten notes and policy PDFs."

---

### Slide 4: Why Current Solutions Fail & Problem Prioritization (1:50 – 2:50 | Presenter 1)
#### Real-World Facts Cited
* **HKFI IFPCD (powered by Shift Technology)**: Focuses on cross-insurer network fraud detection *after* claims are digitized, leaving a gap at **frontline multimodal intake & clause verification**.
* **Air Canada Precedent (2024 BCCRT 149)**: Legal liability when unconstrained chatbots hallucinate policy terms.

#### English Verbatim Script
> "To fight syndicates, the HKFI launched the **IFPCD** database powered by Shift Technology, which detects cross-insurer fraud networks. However, IFPCD relies on structured data *after* intake—it does not solve the frontline adjuster's daily bottleneck of parsing handwritten English-Chinese doctor notes or checking 80-page policy exclusions.
> Legacy OCR breaks on layout changes, while unconstrained LLM chatbots risk **Air Canada-style legal liability** if they hallucinate coverage promises. Using the **Jobs-To-Be-Done** and **2×2 Matrix** from Lecture 1, we target the high-value, controlled-complexity green quadrant: a bounded multimodal triage harness with mandatory human sign-off."

---

## Part 2: Proposed GenAI Solution & Demo (Total: 7 Minutes | 2:50 – 9:50)

### Slide 5: High-Level Architecture — The 4-Stage Deterministic Harness (2:50 – 4:20 | Presenter 2)
#### English Verbatim Script
> "Thank you. Moving to our solution: in Lecture 2 and 3, we learned that a foundation model is only as reliable as the **Harness** around it. As shown by the $\tau$-bench $\text{pass}^k$ metric, an autonomous agent with 90% single-step accuracy drops to 43% reliability over an 8-step chain.
> To prevent compounding errors, ClaimGuard AI decomposes triage into a **Four-Stage Deterministic Pipeline**: Stage 1 extracts multimodal facts; Stage 2 invokes internal databases and policy clauses via the **Model Context Protocol (MCP)**; Stage 3 computes payout math and risk scores; and Stage 4 enforces a strict JSON schema contract before routing to Straight-Through Processing or a Human Adjuster."

---

### Slide 6: Model Selection & Justification — Hybrid 3-Tier Routing (4:20 – 6:10 | Presenter 2)
#### English Verbatim Script
> "Rather than picking one model off a saturated leaderboard, we engineered a **Three-Tier Hybrid Routing Architecture** balancing latency, cost, and Hong Kong data privacy:
> First, for Stage 1 intake, **Gemini 3.5 Flash** uses native multimodality to read handwritten bilingual notes and check image tampering in one pass at sub-second TTFT.
> Second, for the 80% routine policy verification in Stage 2 and 3, we self-host the open-weight **DeepSeek V3 Pro** inside an air-gapped local VPC. This ensures sensitive patient medical records never leave the insurer's premises, complying with Hong Kong's **Personal Data (Privacy) Ordinance (PCPD)** while cutting inference costs.
> Third, only the 20% complex pre-existing exclusions or fraud alerts are anonymized and escalated to **Gemini 4 Hydrogen** for deep reasoning—chosen over Anthropic Claude due to Hong Kong regional availability and enterprise Zero Data Retention compliance."

---

### Slide 7: Data Governance, MCP Grounding & Security Controls (6:10 – 7:30 | Presenter 2)
#### English Verbatim Script
> "To eliminate hallucinated payouts, we enforce two hard controls. First, an **Evidence Chain**: our Hybrid RAG and MCP tools require every decision to cite the exact policy section ID and verbatim quote—otherwise it must abstain and escalate.
> Second, **Authority Containment**: modeled on **Allianz's Project Nemo** human-in-the-loop principle, even if a receipt contains a prompt injection, the LLM has zero API permission to release payouts at or above 5,000 HKD, and **never autonomously rejects a claim**—all adverse decisions require a licensed human adjuster's signature."

---

### Slide 8: Prototype Walkthrough — 3 Simulated HK Scenarios (7:30 – 9:50 | Presenter 3)
*(Open `ClaimGuard_Demo/index.html` on screen or play the screen recording while speaking)*
#### English Verbatim Script
> "Now let's walk through our working ClaimGuard AI prototype across three simulated scenarios modeled on real HKFI and ICAC fraud typologies.
> In **Scenario 1 (CLM-2026-8841)**, a simulated 2,450 HKD outpatient claim is parsed by Gemini 3.5 Flash, verified against doctor registration via MCP, matched verbatim to Policy Section 4.2(a), and approved for **2,025 HKD** under Straight-Through Processing.
> In **Scenario 2 (CLM-2026-8849)**, an 18,600 HKD lumbar MRI claim triggers an MCP cross-check revealing a prior 2024 physiotherapy record before policy inception. Escalated to **Gemini 4 Hydrogen**, it cites **Section 7.3(b) Pre-existing Exclusion**, locks auto-payout, and generates a review brief for a human adjuster.
> Finally, in **Scenario 3 (CLM-2026-8902)**—inspired by real ICAC fake-receipt prosecutions—Gemini's forensic layer flags Error Level Analysis tampering on a Photoshopped trailing zero (4,680 altered to 46,800 HKD) plus a recycled crash photo hash, executing a hard freeze for the Special Investigation Unit. Plus, our workbench includes a **Live Gemini API mode** where we can upload any real receipt image on the spot for real-time multimodal JSON extraction. *(Note: While production deploys Stage 2 on-premises with DeepSeek V3 Pro, this live browser demo routes Stage 1 & 2 through Gemini API for portability, followed by real deterministic JS math and authority gates in Stage 3 & 4.)*"

---

## Part 3: Evaluation & Business Impact (Total: 4 Minutes | 9:50 – 13:50)

### Slide 9: Real-World Industry Benchmarks & Evaluation Plan (9:50 – 11:50 | Presenter 3)
#### Real-World Benchmarks Cited
* **Allianz Project Nemo**: 7 AI agents + HITL cut routine claim processing time by **~80%** (days to hours).
* **AXA RAG & Claims AI**: Cut policy research from **10 mins to <3 mins** (70% faster; 86% user confidence); AI workflows reached up to **60% automation** and **~3% lower losses**.
* **Zurich Insurance**: NLP claim review achieved **58x speed-up** and contributed to reducing annual leakage/errors by **upwards of US$40M**.

#### English Verbatim Script
> "Because we do not have access to confidential production patient records, we anchor our performance expectations on **verified public benchmarks from global tier-one insurers** and pair them with a contamination-free test design.
> In production, **Allianz's Project Nemo**—using a similar multi-agent plus human-in-the-loop pattern—cut routine claim processing time by **80%**. **AXA** cut policy document research from 10 minutes to under 3 minutes using RAG, while **Zurich** achieved a **58x speed-up** on unstructured claim reviews and reduced annual leakage by over **40 million USD**.
> For our own prototype evaluation, to avoid Data Contamination Risk (DCR), we design a synthetic-realistic stress test with custom policy effective dates and MCP state transitions never seen on the public web, enforcing 0% ungrounded citations via strict schema validation."

---

### Slide 10: Illustrative Financial ROI Model (11:50 – 13:50 | Presenter 4)
#### English Verbatim Script
> "To translate those industry benchmarks into a Hong Kong business case, we built an **illustrative sensitivity model** scaled to a mid-sized HK insurer handling **120,000 claims per year**—roughly 0.4% of Hong Kong's direct general claims market.
> Assuming a baseline of 45 adjusters costing 21.6 million HKD annually and 6.5% leakage costing 8.4 million HKD: applying a conservative **75% triage time reduction**—below Allianz's 80% benchmark—frees 30 FTEs of capacity worth **14.4 million HKD per year**. Reducing leakage from 6.5% to 1.4%—aligned with Shift Technology and AXA's 3 to 5% loss-ratio gains—recovers **6.12 million HKD annually**, totaling **20.52 million HKD in annual value**. Against an estimated **3.2 million HKD** Year-1 build and VPC hosting budget, the illustrative first-year ROI is **541%** with a **1.9-month payback**."

---

## Part 4: Future Work & Recommendations (Total: 2 Minutes | 13:50 – 15:00)

### Slide 11: Ongoing Monitoring & Rollout Roadmap (13:50 – 15:00 | Presenter 4)
#### English Verbatim Script
> "Finally, deploying GenAI in Hong Kong insurance requires continuous governance aligned with the **NIST AI Risk Management Framework** and **HK Insurance Authority Guideline 10** on fraud controls. Under MEASURE, we mandate weekly blind human audits on 5% of auto-approved claims to catch billing-code drift. Under MANAGE, we run quarterly red-teaming against emerging deepfake receipt generators.
> We recommend a 12-month phased rollout: 3 months in Shadow Mode, launching live STP under 5,000 HKD in Month 4, and integrating our Stage 2 MCP layer directly with **HKFI's IFPCD database** and standardized VHIS medical coding by Month 12. Thank you, and we welcome your questions!"

---

## Slide 12: Q&A Defense Cheat Sheet (For Live Q&A)
1. **Q: "Where did your numbers come from? Did you really test this on 500 real HK patients?"**
   * **A**: "No—to protect patient privacy and avoid fabricating clinical data, our macro figures come directly from **IA 2024 statistics** and **HKFI/ICAC public reports**, our efficiency benchmarks come from **Allianz, AXA, and Zurich's published case studies**, and our ROI and demo scenarios are transparent **illustrative simulations** built on those real-world parameters."
2. **Q: "How does ClaimGuard AI fit with HKFI's existing IFPCD system?"**
   * **A**: "IFPCD detects cross-insurer fraud networks *after* claims are structured and uploaded. ClaimGuard AI sits *upstream* at frontline intake—converting messy handwritten bilingual notes and receipts into verified JSON, checking policy exclusions via RAG, and feeding cleaner signals into IFPCD."
3. **Q: "How do you comply with HK PCPD privacy and fair treatment rules?"**
   * **A**: "80% of policy reasoning runs inside an on-premises VPC using open-weight `DeepSeek V3 Pro` so medical PII never leaves the insurer, and Stage 4 strictly forbids autonomous rejections—every adverse decision is reviewed and signed by a licensed human adjuster."
