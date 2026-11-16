# ClaimGuard AI — Multimodal Agentic Insurance Claims & Fraud Triage

**CityU IS5542: Generative AI in Business (2026 Sem A) — Final Group Project**

## Deliverables Included
1. **Final Presentation Deck**: `IS5542_ClaimGuard_AI_Final.pptx` (12 slides with embedded speaker notes, native comparison tables, and Gemini-generated visuals).
2. **Interactive Web Prototype**: `ClaimGuard_Demo/index.html` (Zero-dependency enterprise InsurTech workbench supporting **3 simulated HK scenarios** + **Live Google Gemini API** real-time receipt upload with deterministic math & authority gatekeepers).
3. **15-Minute Speaker Script**: `Speaker_Notes_15min_Script.md`.
4. **Test Receipt Samples**: `test_samples/` (`sample_valid_receipt.jpg` & `sample_suspicious_receipt.jpg`).

## Architecture Highlights
- **Tier 1 (Intake Vision & Forensics)**: `Gemini 3.5 Flash` (`gemini-2.5-flash` in Live API mode)
- **Tier 2 (80% Standard Policy Matching)**: `DeepSeek V3 Pro` (On-Premises HK VPC for PCPD compliance)
- **Tier 3 (20% Complex & Fraud Escalation)**: `Gemini 4 Hydrogen`
- **Deterministic Harness**: Arithmetic consistency verification (`itemized_sum_hkd === claimed_hkd`), closed policy citation library (`Sec 4.2(a)`, `Sec 7.3(b)`, `Sec 11.1`), and hard Human-in-the-Loop (HITL) authority containment above `HK$5,000` or `Risk >= 20`.
