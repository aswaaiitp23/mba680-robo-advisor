# Robo-Advisory / Behavioral Portfolio Project (MBA680 Assignment 2) — Summary

MBA680 Assignment 2, six steps: (1) peer group, (2) risk/time questionnaire, (3) BFI-2 personality, (4) utility/value-function questionnaire with mathematical formulation AND graphical representation, (5) EUT and SP/A-BPT portfolio per person using Problem Statement 1 (Markowitz project) inputs, (6) personality commentary. Deliverables: (a) report, (b) interactive robo-advisory portal. A 10-minute in-class presentation was added on 2026-10-05.

**Authoring group (two people): Adwaaiit Pande and Ayushi Mishra.** Distinct from the 4-person Markowitz Portfolio Project group (Adwaaiit, Ayushi, Divyanshu Kumar Gautam, Sonakshi Tyagi). Results are LOCKED at 5 respondents (user decision, 2026-10-05): Shree Charan, Kshitij, Kartika, Ayushi Mishra, Adwaaiit Pande. The user asked for all "who didn't submit" mentions (Divyanshu/Sonakshi) to be removed from the report and portal; do not reintroduce them.

## Status (2026-10-05): everything delivered
- **Report** `MBA680_RoboAdvisory_Report.docx`, 27 pages, written in first person plural ("we/our") at the user's request. Adds Section 3.5 (Figures 3.1–3.4: utility, value, Prelec weighting and β–δ discount curves for all 5), Figure 4.1 (EUT risky share vs γ), Section 6 now documents the evaluation view, and Section 7 has a new γ-identification limitation. TOC is manual (dot leaders); page numbers auto-corrected by a script that searches `pdftotext` output.
- **Portal** https://claude.ai/artifact/GBBbf2PqceCFmkZ4mHihhU, Version 7. It adds inline-SVG Step-4 curves to the individual results screen and the evaluation view (colors are bound to each person, matching the report and deck) and an identification-caveat key finding. "Didn't submit" text removed. All test suites pass (portfolio parity, pooling parity, jsdom DOM tests including curve checks).
- **Presentation** `MBA680_Assignment2_RoboAdvisory.pptx`, 14 slides on the user's template (the Microsoft "Product pitch deck" design, turquoise #3AEFCC, Arial Black / Avenir). Native charts and tables. Adwaaiit presents slides 1–6 (approach, instruments, engine, the two Step-4 graph slides), Ayushi presents 7–13 (divider, outcomes table, EUT, BPT, personality, portal screenshots, summary), and both take the close. Each slide's notes carry a full script with timings plus Q&A backup on the final slide. The portal appears as screenshots only (user choice).
- **Submission zip** `MBA680_Assignment2_Final.zip`: report and deck, plus report_source/ (docx-js), portal_source/, python_pipeline/ (14 pytest pass), step4_graphs/ (make_graphs.py, PNGs, parameters CSV) and presentation_source/build_deck.py.

## Key numbers (pooled; from pipeline/outputs CSVs)
| Person | G-L | γ | λ | α | β | δ | BPT safety | BPT ret / vol |
|---|---|---|---|---|---|---|---|---|
| Shree Charan | 27 | 2.21 | 1.000 | 0.57 | 0.80 | 0.944 | 30.0% | 16.19% / 29.46% |
| Kshitij | 31 | −0.50 (floored 0.05) | 1.600 | 0.40 | 0.63 | 0.900 | 40.0% | 15.77% / 27.12% |
| Kartika | 31 | 0.20 | 1.000 | 1.00 | 0.90 | 0.930 | 30.0% | 16.19% / 29.46% |
| Ayushi | 35 | 2.21 | 1.009 | 1.09 | 0.76 | 0.945 | 30.2% | 16.19% / 29.42% |
| Adwaaiit | 40 | 2.19 | 1.015 | 1.25 | 0.94 | 0.976 | 30.3% | 16.18% / 29.40% |
EUT: everyone 100% in the tangency portfolio (13.21% return, 16.08% volatility), since λ_mkt/γ > 1 with λ_mkt = 2.5. Standard-λ Black-Litterman universe: 66 NSE stocks, rf 6.75%.

## New finding (2026-10-05): γ is only partially identified
The engine floors the value exponent 1−γ at 0.05, so γ grid points 1.6, 2.3 and 3.0 give identical choice likelihoods. The γ ≈ 2.2 for Shree Charan, Ayushi and Adwaaiit is therefore effectively the mean of indistinguishable points: we know γ is above about 1, not its exact size. At γ = 3.0 the EUT risky share would be 83%, so EUT saturation for those three is conditional. This is disclosed in the report (Section 7, Figure 4.1), the portal and the deck.

## Other self-report vs revealed gaps
Adwaaiit: self-rated risk 10/10 and the top Grable-Lytton score (40), yet γ ≈ 2.2; self-rated patience 4/10, yet he is the most patient (D(365) = 0.70). Shree Charan: flat 3.00 on BFI-2 (likely straight-lining). Ayushi: retest 0.5.

## Files (container is not persistent; the zip is the durable copy)
/home/claude/{roboadvisory_report, webapp, pipeline, step4_graphs, deck}. Rebuild the report with `node main.js`, the graphs with `python3 make_graphs.py`, and the deck with `python3 build_deck.py` (needs skeleton.pptx, made from the template via add_slide.py: slide order 1, 9, 10, 8, 11, 11×2, 7, 11×3, 6→Title-and-Content layout, 11, 12, 13). The live portal artifact is the source of truth for survey.html.
