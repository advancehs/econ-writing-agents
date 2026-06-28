# Econometric Writing Principles

Distilled from empirical economics practice (causal inference, panel data, applied microeconomics, international trade & political economy), thesis/paper supervision, and Michael Black's "Writing a Good Scientific Paper".
Canonical reference — all agents and workflows consult this file.
Organized into 8 categories that map to agent specializations.

---

## A. Structure & Narrative

*Primary agents: logic-reviewer, consistency-checker*

### A1. Recursive Consistency Checks
For each chapter, section, and subsection — verify that terminology, the stated roadmap, the actual flow, and the empirical results all match. If a section says "we discuss X, Y, Z," the subsections must cover exactly X, Y, Z in that order.

**Common violations**: Section intro promises three mechanisms but delivers two; subsection order doesn't match the intro's enumeration; terminology drifts between sections (e.g., "treatment" vs "exposed group" vs "BRI countries" used interchangeably without definition).

### A2. Logical Chaining with Transitions
Every paragraph, section, and chapter should be "chained" logically. The end of one section should motivate the start of the next. Never leave two adjacent paragraphs without a transition. Paragraph-to-paragraph connections are the more common failure mode.

**Common violations**: Abrupt shifts from institutional background to a regression table with no bridge; a results subsection that starts with no connection to the identification setup that preceded it; adjacent paragraphs on related subtopics connected only by thematic proximity rather than explicit bridging.

### A3. Table/Figure Definition Order
Ensure that table/figure definition order in the source matches the order they are first mentioned and discussed in the text.

**Common violations**: LaTeX source defines Table 5 before Table 3; an event-study figure is `\input`'d early but not discussed until pages later.

### A4. Close Every Paragraph
The last sentence of a paragraph should conclude, synthesize, or motivate the next paragraph — not trail off. A strong closer draws an implication, states an economic mechanism, or poses a question the next paragraph answers.

**Common violations**: Paragraphs ending with "which we discuss below" or a bare coefficient; final sentences that drop a new statistic without interpretation; paragraphs that simply stop after the last piece of evidence.

### A5. Claim-First Exposition
State the conceptual contribution or finding before diving into technical details. The reader should know *what* and *why* before *how*. The first 1–2 sentences of each section should declare the goal before presenting the specification or table.

**Common violations**: Results sections that open with "Column (1) of Table 3 reports..." before stating what the table establishes; empirical-strategy sections that dive into the DID specification before stating what causal effect is being identified.

### A6. Goal-Problem-Solution Rhythm
Every section should follow a Goal-Problem-Solution (GPS) rhythm. **Goal**: what effect/question are we after? **Problem**: what confounds it / why is identification hard? **Solution**: what design (DID/IV/RDD/event study) resolves it? Sections that jump to regressions without establishing the identifying challenge lose the reader.

**Common violations**: Identification sections that present the two-way fixed effects spec without first stating the endogeneity concern it addresses; introductions that list findings without establishing the gap in the literature.

### A7. The Nugget — One Key Finding Per Paper
Every paper should orbit a single key finding — the "nugget" — that the reader takes away. All specifications, robustness checks, and figures should serve this central result. If you cannot state the nugget in one sentence, the paper's focus is unclear.

**Common violations**: Papers that present a battery of coefficients without a unifying takeaway; abstracts that list estimation methods rather than the economic effect estimated; conclusions that enumerate every robustness column rather than crystallizing the magnitude and mechanism.

---

## B. Prose & Style

*Primary agents: writing-reviewer, prose-polisher*

### B1. Avoid Exhaustive-Sounding Enumerations
When listing examples, use "such as" rather than "for" to avoid implying the list is complete. ("robust across sectors such as manufacturing and services" rather than "robust across sectors manufacturing and services".)

**Common violations**: "for" used with partial lists; enumerations of countries/sectors that imply completeness when illustrative.

### B2. Avoid Negation-Contrast Structures
Rephrase "not X, but Y" / "not because... but because..." positively. These are a strong AI-writing marker. E.g., "not because the channel is absent, but because the data cannot isolate it" -> "the data cannot isolate the channel, so the coefficient is uninformative about it."

**Common violations**: Sentences structured around negation before stating the point; double negatives; "not only... but also" used excessively.

### B3. Avoid Colloquial Terminology in Titles/Formal Claims
Vivid phrases can appear parenthetically but should not be primary terminology. Use formal econometric terms in titles and section headings; introduce colloquial shorthand once parenthetically.

**Common violations**: Informal shorthand ("the trade-war hit") as a section title; metaphorical labels presented as formal variable definitions.

### B4. Match Discussion Tone to Author Voice
Results and discussion should flow as analytical prose (claim -> evidence -> mechanism -> robustness -> implication), not flat report-style enumeration of coefficients. The author's voice is deductive, first-person plural, active, with calibrated hedging. See the project CLAUDE.md for the full style profile.

**Common violations**: Bullet-point style findings; flat enumeration of "Column (1): 0.23, Column (2): 0.31" without analytical depth; discussion sections that read like a table read-aloud rather than an argument.

### B5. One Idea Per Sentence
Split sentences that pack multiple distinct claims. Each sentence should advance exactly one point. If a sentence needs "while", "unlike", or a semicolon to stitch together separate claims, it should be two sentences.

**Common violations**: Sentences like "Unlike prior work which uses cross-sectional OLS, we employ a stacked DID and find a positive significant effect"; compound sentences where each half could stand alone.

### B6. Calibrated Confidence Language
Use assertive language for reported numerical results ("the coefficient is 0.234, significant at the 1% level") and hedged language for causal interpretation ("this *suggests* that BRI exposure *increased* trade", "we *interpret* this as evidence of..."). Do not hedge reported statistics; do not assert causal mechanisms that the identification strategy does not support. See G3.

**Common violations**: "may" / "might" / "could" modifying reported coefficients or p-values; "because" / "leads to" / "drives" used with assertive tone for mechanisms not pinned down by the identification; "proves" / "shows definitively" for estimates that are still associational under the chosen design.

### B7. Ruthless Conciseness
Every word must earn its place. Cut filler ("it is important to note that", "in the context of"), compress relative clauses, and prefer short words over long Latinate ones when meaning is preserved ("use" not "utilize", "show" not "demonstrate").

**Common violations**: "It is worth noting that" (cut entirely); "in order to" -> "to"; "a large number of" -> "many"; "due to the fact that" -> "because"; padding with "importantly", "interestingly", "notably".

### B8. AI-Writing Tell Detection
Actively scan for and eliminate patterns that mark text as AI-generated. Common tells: (1) "not X, but Y" negation-contrast (B2), (2) "delve", "leverage", "landscape", "tapestry", "multifaceted", "paradigm shift", "navigate the complexities of", (3) sentences starting with "Moreover", "Furthermore", "Additionally" in sequence, (4) formulaic transitions ("Building on this", "Against this backdrop"), (5) hollow intensifiers ("crucial", "vital", "essential" used interchangeably), (6) mirroring the user's exact phrasing, (7) overly balanced "on one hand / on the other hand". Replace with direct, specific language.

**Common violations**: Three consecutive paragraphs starting with "Moreover"/"Furthermore"/"Additionally"; "delve into the mechanisms" instead of "examine the mechanisms"; "the landscape of global trade" as vague framing.

---

## C. Econometric Equations

*Primary agents: technical-reviewer, identification-reviewer*

### C1. Equations for Clarity, Not Complexity
Use formal notation to make the estimating equation precise, but notation should *clarify*, not overwhelm. Define every symbol before first use; keep subscript conventions consistent (typically i for unit, j for partner/sector, t for time). No more than two new symbols per sentence.

**Common violations**: Indices introduced without explanation (e.g., $Y_{ijt}$ with $i,j,t$ undefined); inconsistent subscripts across the equation and the table (equation uses $ijt$, table header says "country-year"); over-formalizing a simple OLS that a sentence would convey better.

### C2. Text–Equation–Table Triple
A core specification deserves explanation through all three modalities: intuitive text (what is being estimated and why), the formal equation (the precise functional form and identifying variation), and the regression table (the estimate). The three must reinforce each other — the table's column should map to the equation, and the prose should interpret the table's coefficient in the equation's terms.

**Common violations**: A table reports interaction-term coefficients but the equation shown has no interaction; prose says "the DID coefficient is positive" without mapping it to a specific symbol in the equation; the equation includes fixed effects the table footnote omits.

### C3. Equation–Code Correspondence
The estimating equation's symbols must map clearly to the variables in the Stata `do`-file / Python data-construction script and to the column labels in the table. If the equation writes $\beta \cdot \text{Treat}_{ij}\times\text{Post}_t$ but the code calls it `bri_post` and the table labels it "BRI × Post", state the mapping explicitly. Readers (and replicators) should not reverse-engineer it.

**Common violations**: Equation uses $\tau$ for the treatment effect while the table labels the same coefficient "BRI_intl" with no mapping noted; the data script constructs `distort_mt` but the paper never defines which distortion measure it is; FE dummies in the code (`i.cid#i.py`) that the table footnote describes differently.

---

## D. Tables & Figures

*Primary agents: consistency-checker, latex-layout-auditor, regression-table-auditor, latex-figure-specialist*

### D1. Active Use of Tables and Figures
Use tables and figures to carry the empirical weight. Regression tables report the estimates; event-study figures establish pre-trends; coefficient plots summarize heterogeneity. Consider whether every major empirical claim has adequate tabular or visual support.

**Common violations**: Long stretches of prose describing coefficients that belong in a table; event-study results reported only numerically rather than plotted; heterogeneity discussed in text without a coefficient plot or split-sample table.

### D2. Cross-Reference All Floats
Never let any table or figure "just be there." Every float must be explicitly referenced (`\ref`/`\cref`) and its content discussed in the surrounding text.

**Common violations**: Tables placed in the document but never cited with `\ref`; a figure referenced once ("see Figure 3") with no discussion of the pre-trend pattern it shows.

### D3. Table/Figure–Text–Note Consistency
Match what the table shows, what its notes say, and what the body text claims. If they describe the same coefficient differently, reconcile them.

**Common violations**: Body text reports a coefficient as 0.234 but the table shows 0.23 (rounding not reconciled) or a different column; notes say "clustered at the country level" but the specification clusters at the pair level; a figure's x-axis labels don't match the years discussed in text.

### D4. One Table, One Message
Do not layer multiple unrelated stories onto one table. If a table answers two questions (e.g., baseline effect AND mechanism), consider splitting or clearly paneling it.

**Common violations**: A single table mixing the baseline DID, the IV first stage, and a heterogeneity split with no clear panel structure; an event-study figure that also overlays a placebo group, muddying both messages.

### D5. Interpret Tables/Figures, Don't Just Reference
When referencing a table or figure, tell the reader what to look for. Not just "as shown in Table 3" — say which coefficient, its sign and magnitude, its significance, and what it implies for the identifying claim. This extends D2 (existence of reference) to quality of reference.

**Common violations**: Bare "see Table 3" with no reading of the coefficient; "Figure 3 shows no pre-trend" without naming which pre-period years are jointly insignificant; paragraphs that let the reader extract the table's message unaided.

### D6. Table Layout & Alignment
Use `booktabs` rules (`\toprule`, `\midrule`, `\bottomrule`) for clean three-line tables. Align numerical columns on the decimal; right-align or center statistics; keep column headers parallel; use `threeparttable` so notes align to the table width. For coefficient plots, align coefficients on a zero reference line.

**Common violations**: `\hline` and `\cline` instead of booktabs rules; columns of unequal precision; notes spilling beyond the table width; significance stars not aligned under their coefficients.

### D7. Note Self-Sufficiency
A table/figure note should be understandable without the body text. It should state the dependent variable, the key regressor, the fixed effects included, the clustering level, the sample size (N), the meaning of significance stars (* p<0.10, ** p<0.05, *** p<0.01), and the data source. Readers often scan tables and notes before reading the text.

**Common violations**: Notes missing the FE list or clustering level; notes that omit the star legend; notes that say "see text for variable definitions" for the central regressor; dependent variable undefined in the note.

---

## E. Citations & Bibliography

*Primary agents: technical-reviewer, bibliography-auditor*

### E1. Cite Named Datasets and Methods
Cite named datasets (UN Comtrade, CEPII BACI, WIOD, Penn World Table, World Bank WDI/Governance, etc.) and named econometric methods (difference-in-differences, instrumental variables, regression discontinuity, synthetic control, shift-share/Bartik, Callaway-Sant'Anna, de Chaisemartin-D'Haultfœuille, Sun-Abraham) at first use in each section, even if cited earlier.

**Common violations**: "Comtrade bilateral trade data" with no citation in the data section; "we use a stacked DID estimator" with no methodological citation; an instrument introduced without citing its construction source.

### E2. Citation Completeness at First Mention
Cite foundational and methodological references at first mention in each chapter, even if well-known. Readers may start from any chapter.

**Common violations**: "two-way fixed effects" used in a results chapter with no Card-Krupkin/Goodman-Bacon/de Chaisemartin citation; "parallel trends" assumed without citing the canonical treatment; instrument validity discussed without relevance/exclusion citations.

### E3. Bibliography Hygiene
Entries should be complete, consistent, and up-to-date. Check: (1) required fields present (authors, title, year, journal, volume, issue, pages, DOI), (2) title capitalization brace-protected for proper nouns and acronyms (`{BRI}`, `{WTO}`, `{GVC}`), (3) **NBER/SSRN/working-paper citations updated to their published versions** when a journal version exists (a top-journal referee expects the AER/QJE/Econometrica/RES/JPE version, not the 5-year-old working paper), (4) author names consistent across entries, (5) journal names consistent (not "AER" in one entry and "American Economic Review" in another — pick one style), (6) no "?" markers in the compiled PDF. Cross-check against RePEc for canonical entries and DOIs.

**Common violations**: NBER working papers cited when a published version exists; missing DOIs or page numbers; inconsistent journal abbreviations; working-paper titles not updated to the published title; placeholder fields ("forthcoming", "under review") never resolved.

---

## F. Process & Meta

*Primary agents: writing-reviewer (final pass)*

### F1. Strategic Limitation Placement
How and where to discuss limitations depends on the document type. **Journal submissions**: Be strategic — acknowledge the binding constraint briefly and pivot to the research design that addresses it, or frame as future work. Do not enumerate every次要 caveat. **Thesis / internal drafts**: Discuss limitations at the point the design decision is made. In both, lead with the strongest robustness, not the longest apology.

**Common violations**: A limitations paragraph that reads as a numbered confession of nine defects; defensive over-explanation embedded inside each result; limitations placed in the identification section before results build confidence.

### F2. Negation-Contrast Audit
Before finalizing any chapter, search for "not...but" patterns and rephrase positively (per B2). A final-pass grep for `is not.*but`, `not to.*but to`, `not how.*but` catches residual instances.

**Common violations**: "The effect is not driven by X but by Y" (rephrase: "Y drives the effect"); "the goal is not to X but to Y" (rephrase: "the goal is Y: ...").

---

## G. Empirical Identification & Regression

*Primary agents: identification-reviewer, regression-table-auditor, technical-reviewer*

### G1. Identification Strategy First
State the causal estimand and the identifying assumption *before* presenting coefficients. Name the design (DID/IV/RDD/event study/synthetic control), the source of variation, and the comparison group. The reader should know what variation identifies the effect before seeing any number.

**Common violations**: Results sections that report coefficients without restating what identifies them; a "BRI effect" discussed without specifying treated vs control and pre vs post; IV estimates presented without stating the exclusion restriction relied upon.

### G2. Parallel Trends & Pre-trend Tests
For any difference-in-differences or event-study design, report the pre-trend evidence explicitly: the joint test of pre-period coefficients and the individual pre-period point estimates. State clearly when each pre-period year is individually insignificant, not merely that the joint test passes. Bin pre-periods only from the start of the sample, never skipping early years, and never bin post-period years.

**Common violations**: Claiming "no pre-trend" citing only a joint F-test while a single pre-period year is significant; binning 2014–2016 while leaving 2009–2013 granular; binning any post-treatment year; a stacked/event-study figure with no accompanying table of pre-period p-values.

### G3. Calibrated Causal Language
Match causal claims to what the identification supports. Under a credible DID/IV/RDD, "BRI exposure increased trade by X%" is defensible. Under OLS with unaddressed endogeneity, write "is associated with" / "correlates with". Never assert causation the design does not deliver, and never hide behind vague verbs ("affects", "impacts") that smuggle in causality.

**Common violations**: "trade war drives a collapse in exports" from an OLS association; hedging an IV estimate that satisfies relevance and exclusion as if it were still correlational; "impacts" used to imply causality without owning the identification claim.

### G4. Regression Table Completeness
Every regression table must report: the key coefficient(s) with standard errors, fixed effects (listed, not just "FE = yes"), the clustering level, the number of observations (N), the number of clusters, and an R² or within-R². Significance stars follow the standard legend (* 0.10, ** 0.05, *** 0.01) and the legend appears in every table note.

**Common violations**: "Year FE ✓" without listing the FE dimension (country×year vs partner×year matters); standard errors shown but clustering level unstated; N reported but number of clusters omitted; stars present but legend missing from one table.

### G5. Coefficient–Narrative Consistency
The sign, magnitude, and significance of every coefficient you discuss in prose must match the table exactly. Report standard errors or p-values alongside. If a coefficient is insignificant, say so — do not narrate its sign as if it were significant, and do not narrate a significant coefficient as "suggestive". Direction constraints the author has committed to (e.g., the headline effect must be positive and significant; no post-period year may be significantly negative) must hold in both table and text.

**Common violations**: Prose calls a coefficient "positive and significant" when it is insignificant or negative in the table; magnitude rounded inconsistently between text and table; a direction constraint violated silently (e.g., a post-period year significantly negative reported without flagging the conflict); treating an insignificant distortion coefficient as if it carried the same weight as the significant headline coefficient.

---

## H. Paragraph-Level Flow & Self-Audit

*Primary agents: writing-reviewer, prose-polisher, section-drafter, logic-reviewer*

> Adapted from [Master-cai/Research-Paper-Writing-Skills](https://github.com/Master-cai/Research-Paper-Writing-Skills), which distills Peng Sida's open research-writing notes. These are cross-disciplinary, paragraph-level tools.

Categories A–G govern the manuscript (A), the sentence (B5), and the empirical claim (G). This category fills the **paragraph** layer — the unit a reader actually traverses — with portable flow and self-audit tools.

### H1. One Message Per Paragraph
Each paragraph carries exactly one claim, finding, or step of the argument. If a paragraph does two things (e.g., reports a coefficient *and* launches a mechanism story), split it. A reader should be able to state each paragraph's message in one sentence after reading it.

**Common violations**: Results paragraphs that open with the baseline coefficient, pivot mid-paragraph to heterogeneity, then close on a robustness check — three messages fused; literature paragraphs that interleave "what we do" with "what others did" instead of dedicating one paragraph to each.

### H2. Topic-Sentence-First (Paragraph Level)
The first sentence of each paragraph states the paragraph's message; the rest supplies evidence, mechanism, or qualification. This is the paragraph-level analogue of A5 (which governs sections). Do not bury the point in the middle or defer it to the end with no forewarning.

**Common violations**: Paragraphs that build context for three sentences before stating the finding; topic sentences that are pure transition ("Another important result is...") carrying no content; the message hidden in the final sentence.

### H3. Self-Contained Terminology
Make every key noun readable without hidden context: define a new term at first use and use it consistently (do not rotate synonyms — see A1). A reader landing mid-section should not need to scroll up to decode a term.

**Common violations**: "the exposure variable" used before "BRI_intl" is defined; "treated units" introduced without saying treated by what and when; an acronym (e.g., "GVC") used pages before its expansion.

### H4. Reverse Outlining
After drafting a section, run a reverse outline to stress-test its logic: (1) write the section's thesis/nugget (A7); (2) write each paragraph's topic sentence (H2); (3) under each, note the evidence/estimation it offers; (4) check every topic sentence maps to the thesis and every evidence point maps to its topic sentence; (5) revise or delete any paragraph that fails the mapping. If the reverse outline is hard to write, the thesis or topic sentences are unclear.

**Common violations**: A results section whose reverse outline reveals two paragraphs with the same topic (merge) or a topic sentence with no supporting coefficient (cut or re-evidence); identification sections where a paragraph's "evidence" is actually a method choice with no identifying claim attached.

### H5. Reader-Perspective Self-Check
Read the draft as an uninformed but expert reader. For each paragraph ask: Would a peer outside this project understand the vocabulary? Does the paragraph visibly connect back to the identification strategy or the nugget? Is the take-away obvious to someone who did not run the regressions?

**Common violations**: Paragraphs intelligible only to the author (who knows the data); a discussion that assumes the reader recalls the FE structure from three pages back; take-aways that are implied but never stated.

### H6. Transition Lexicon
Bridge every adjacent paragraph and every sentence pair with an explicit relational marker (per A2). Pick the marker that matches the logic, not a generic "Moreover". Reference set:

- Causal / mechanism: because, so, therefore, thus, hence, consequently, as a result
- Contrast / exception: however, but, although, yet, in contrast, nevertheless, instead, on the other hand
- Comparison / extension: similarly, likewise, in the same way, also
- Illustration: for example, for instance, such as, in particular
- Refinement / elaboration: specifically, that is, in other words, more precisely
- Sequence / temporal: first, then, next, finally, before, after, meanwhile

**Common violations**: Adjacent paragraphs joined only by thematic proximity with no marker; "Moreover"/"Furthermore"/"Additionally" repeated in sequence (also an AI-writing tell, B8); causal markers ("therefore") used where the identification supports only association (violates G3).

### H7. Claim–Evidence Mapping
Treat claim–evidence alignment as a hard constraint (the empirical cousin of A5/G5). For each major claim — especially in the abstract and introduction — produce an explicit map: `Claim: <statement> | Evidence: <table/figure/spec/estimate> | Status: supported | needs evidence | overstated`. If a claim's status is "needs evidence", add the evidence or weaken/remove the claim (per F1, strategically).

**Common violations**: An abstract claim ("BRI exposure redirected trade") with no table pointed to; an introduction that asserts a mechanism no section establishes; a "significant" qualifier in the abstract attached to a coefficient that is insignificant in the table (G5).

### H8. Adversarial Self-Review (Economics-Adapted Five Dimensions)
Near submission, read the manuscript as a skeptical referee and answer every question below with explicit evidence, marking each `pass | needs revision | needs new estimation`. Repeat until no major reject-risk remains. These are *self-audit prompts* — questions to interrogate the draft — complementing category G, which states the *principles* the draft must satisfy.

**1. Contribution**

- What new economic knowledge does the paper deliver (a causal effect, a mechanism, a new dataset or lens)?
- Is the identifying variation or the finding genuinely non-obvious, not a predictable re-estimation?
- Can the nugget (A7) be stated in one sentence with its magnitude?

**2. Writing Clarity**

- Could a knowledgeable reader replicate the estimation from the text alone (specification, FE, clustering, sample)?
- Does every section follow the Goal–Problem–Solution rhythm (A6) and state the identifying claim before coefficients (G1)?
- Are terms, notation, and magnitude rounding consistent across text, equation, and table (A1, C3, G5)?

**3. Identification Strength**

- Is the identifying assumption (parallel trends / exclusion restriction / continuity) stated and *defended*, not merely assumed?
- Are the headline coefficients economically meaningful, not just statistically marginal?
- Does causal language match what the design delivers (G3)?

**4. Robustness Completeness**

- Are the key design choices ablated (alternative FE, clustering, control sets, sample windows, placebo / pre-treatment)?
- Are all relevant strong estimators (e.g., Callaway-Sant'Anna, de Chaisemartin-D'Haultfœuille) included under fair settings?
- Are pre-trend tests reported at the joint *and* individual-year level (G2)?

**5. Design Soundness**

- Is the empirical setting realistic for the economic claim being made?
- Are there hidden technical defects or untenable assumptions (e.g., binning that skips early years, post-period binning, sample-end truncation)?
- Is the result robust without per-specification tuning, and do the design's benefits outweigh its limitations (F1)?
