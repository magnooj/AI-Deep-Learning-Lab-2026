# Lab 07 Curriculum & Agenda

**How to Fine Tune a Vision-Language Model** · RSNA 2026 Deep Learning Lab 07 · Wednesday, December 2, 2026 · 8:00–9:00 AM CT · Advanced

> **Status:** Draft v0.1 (Oct 4, 2026). For Ali Ganjizadeh, Julie Bauml and Kalina Slavkova to review.
> **What this is:** a team planning document. It sets the agenda, gives each presenter a scope, and lists shared decisions and deadlines. It does **not** contain the materials. Each presenter writes their own slides or notebook inside the guardrails below.
> **What it isn't (yet):** participant-facing. Before the final PR we decide whether this file stays in the repo (Q7). The README gets a short Agenda table either way.

---

## 1. At a glance

| | |
|---|---|
| **Program** | 45 scripted minutes in the 60-minute slot. The other 15 minutes are reserve (section 2). |
| **Flow** | Kickoff (Ali, 3) → Clinical context (Julie, 8) → VLM and fine-tuning concepts (Ali, 10) → Hands-on notebook (Kalina, 18) → Clinical read of the outputs (Julie, 3) → Wrap-up (Ali, 3) |
| **One running example** | All three segments use the same clinical task, model and 5–6 "anchor" images (D1–D4). This is what makes three talks feel like one lab. |
| **Participant pre-setup** | Laptop, Chrome, a personal Google account. Goal: **no Hugging Face account or token** (only possible if the model is ungated, see D2). |
| **Hard stop** | Content ends 8:58. Room clear by 9:00. |
| **Merge deadline** | **Sun Nov 15, 2026.** After that, only fixes the director flags. No pushes during the meeting. |

| Person | In the room | Produces before the meeting |
|---|---|---|
| **Ali Ganjizadeh, MD MBA** (moderator) | Kickoff, concepts talk, wrap-up; timekeeper for Julie and Kalina; runs Q&A | Kickoff/wrap-up slides, concepts slides, README updates, PRs, contact with the director |
| **Julie Bauml, MD** | Clinical context, clinical read; timekeeper for Ali; roams as clinical helper during the notebook | Clinical slides; vets the anchor images and labels; signs off on the metrics |
| **Kalina Slavkova, PhD** | Hands-on notebook; answers notebook questions | Notebook, executed copy with outputs, precomputed artifacts, backup screen recording |

---

## 2. Agenda (run of show)

| Clock | Min | Segment | Owner | Participants are… |
|---|---|---|---|---|
| 8:00–8:03 | reserve | Doors open; setup slide with QR code and short URL on screen | Ali (Julie and Kalina roam) | Opening the notebook, signing in to Colab, connecting to a T4 GPU |
| 8:03–8:06 | 3 | **Kickoff:** disclosures, faculty, goal, agenda, **"press play on the Setup cell now"** | Ali | Starting the Setup cell (installs and downloads run during the talks) |
| 8:06–8:14 | 8 | **Clinical context:** applications, why fine-tune, what to watch out for | Julie | Listening; Setup cell running in the background |
| 8:14–8:24 | 10 | **VLM and fine-tuning concepts:** anatomy, what fine-tuning changes, the strategies | Ali | Listening; Setup cell finishing |
| 8:24–8:42 | 18 | **Hands-on notebook:** inspect → data → zero-shot → live fine-tune → before/after → failure probes | Kalina | Running cells; anyone behind runs the completed cells or switches to skip-training mode |
| 8:42–8:47 | reserve | **Overflow** for the notebook. If on time: catch-up, hyperparameter exploration, questions | Kalina (Ali makes the call) | Catching up or exploring |
| 8:47–8:50 | 3 | **Clinical read:** a radiologist judges the before/after outputs | Julie (Kalina drives the screen) | Judging the outputs alongside Julie |
| 8:50–8:53 | 3 | **Wrap-up:** take-homes, how to keep going safely, Lab 08 next at 9:30 | Ali | Scanning the repo QR code |
| 8:53–8:58 | reserve | **Q&A** from the parking lot | Ali moderates; all answer | Asking questions |
| 8:58–9:00 | reserve | Hard stop | All | Leaving |

**Why this shape**
- **Setup runs during the talks.** Free Colab needs roughly 5–10 min to install, download and load the model (to be measured in the pilot). Starting it at 8:03 means it's done before the notebook starts at 8:24.
- **Julie goes first**, so the room knows what "good" means clinically before seeing the mechanics. Lab 03 (Mon) covers foundation-model basics, so Ali's definition of a VLM can be brief.
- **The notebook gets the biggest block, with overflow right after it.** It covers LO4 and most of LO5, and it is the segment most likely to run long.
- **Julie closes the notebook** with a short clinical read. It ties evaluation (LO5) back to clinical judgment and gives the lab a clear ending. *(This addition is beyond the original outline; drop it if the team prefers.)*
- **Reserve: 15 min** = 3 at the doors + 5 overflow + 5 Q&A + 2 margin.

---

## 3. Who owns what (no-overlap rules)

Each concept is **explained once** by its owner. Everyone else **refers back** to it ("as Ali showed…") and doesn't re-teach it.

| Topic | Owner explains it | Others may only… |
|---|---|---|
| Where VLMs help in radiology; when to fine-tune vs prompt, RAG or an off-the-shelf model | Julie | Ali: one line that prompting is always the baseline |
| What a VLM is; its components; how an image becomes tokens | Ali | Kalina: show the same parts in the "inspect model" cell, using the same labels |
| Full fine-tuning vs LoRA vs QLoRA vs prompt tuning | Ali | Kalina: point to the config objects that implement them |
| Why overfitting and forgetting happen | Ali | Kalina: show them; Julie: the clinical consequence |
| Data quality, labels, dataset composition (concepts) | Julie | Kalina: how it looks in our dataset (splits, leakage, label conventions) |
| Clinical error types (hallucinated findings, laterality, negation) | Julie | Ali: the mechanism in one line; Kalina: the probe that tests for it |
| Which metric fits which clinical task | Julie | Kalina: computes those metrics, **using the same names** |
| Running the code, hyperparameters in practice | Kalina | none |
| Regulatory status | Julie (one slide or line) | none |

**Out of scope for the whole lab** (point elsewhere instead):
- DICOM retrieval, de-identification, cohort building → **Lab 08 (today, 9:30)**
- Deployment monitoring and drift → Lab 04
- Operating-point selection → Lab 06
- Attention maths, tokenizer algorithms, distributed training → not covered

**Rules for everyone**
- Keep content vendor-neutral: no HOPPR product demos. Follow RSNA's disclosure rules (Q4).
- Every model output shown on a slide must be a real output from our notebook on a free T4. No invented examples.
- Use **"VLM"** throughout, and say once that the README's "LVLM" means the same thing.
- Backup slides stay in backup. If a topic isn't on your MUST list, it only comes up in Q&A.

---

## 4. Segment briefs

Each brief gives the **time box, goal, LOs owned, MUST / NICE / OUT, take-homes, deliverable, hand-off and cut-first**. The content is yours to write.

### 4.1 Ali: moderator (kickoff 3 min, wrap-up 3 min)

- **Goal:** every laptop is running the Setup cell by 8:06, the clock is kept, and the lab ends on time with safe next steps.
- **Kickoff MUST:** disclosures; faculty and their roles; one-sentence goal; agenda; setup instructions (open the notebook → sign in → connect T4 → press play on the Setup cell); how to ask for help (raise a hand or put up a sticky note for setup problems; concept questions go to the parking lot and are answered at 8:53).
- **Wrap-up MUST:**
  - one take-home per segment;
  - how to keep going safely: re-run on public data, and fine-tune on institutional data only with IRB and data-governance approval, on approved compute, never in a personal Colab;
  - pointer to Lab 08 at 9:30;
  - repo QR code.
- **OUT:** new content in the kickoff or wrap-up.
- **Deliverable:** `Slides_0_Kickoff_and_Wrap_Up.pdf`, about 4 kickoff and 3 wrap-up slides. Put the QR code and short URL on the first and last slide.
- **Suggested hand-off to Julie:** "Before we touch any code, the question every radiologist asks: would I trust this output?"
- **Cut first:** say the agenda instead of showing it; shrink the wrap-up to the take-home slide.

### 4.2 Julie: clinical context (8 min) and clinical read (3 min)

- **Goal:** show where VLMs help radiologists today, when fine-tuning is the right tool, and how a radiologist decides whether to trust an output.
- **LOs owned:** **LO3** (primary); the clinical side of LO1, LO2 and LO5.

**MUST cover**
1. **Hook:** a real, cited example of a model output a radiologist would not sign.
2. **Landscape:** where VLMs are used or piloted (report drafting is the most mature; also VQA, findings classification, triage, structured output). One line on regulatory status, re-checked in mid-November.
3. **When to fine-tune:**
   - Prompting is the first baseline.
   - Use RAG (retrieval) when what's missing is text knowledge.
   - Fine-tune for new behavior or output format, local visual skill (your scanners, population), a smaller or on-prem model, or house style.
4. **Data and labels (LO3):**
   - the label is the curriculum;
   - reader variability;
   - dataset composition and shortcuts;
   - train/test leakage;
   - subgroup performance;
   - governance: weights fine-tuned on patient data can memorize it, so treat the adapter as protected data.
   - Use one example from our dataset (Kalina can supply it).
5. **Clinical error types:** hallucinated or missed findings, wrong laterality, flipped negation, wrong severity.
6. **Metric by task:** accuracy, sensitivity and specificity for closed questions; exact match for short answers; why BLEU/ROUGE miss clinical errors in reports. Name clinical report metrics (e.g. GREEN, RadGraph F1) but don't teach them.
7. **A short "would I trust this?" checklist** (4–6 questions). It's reused in the clinical read.

- **NICE (backup):** named medical VLMs (e.g. MedGemma, CheXagent, MAIRA-2); published error rates; EU AI Act and FDA PCCP timing; reporting guidelines (TRIPOD-LLM).
- **OUT:** VLM internals, tokens, LoRA (Ali); code and metric computation (Kalina); DICOM and de-identification (Lab 08).

**Clinical read (8:47–8:50)**
- No new slides; Kalina keeps the before/after on screen.
- Apply the checklist to 1–2 anchor cases. Name one real failure (ideally one a participant found).
- One line on automation bias.
- One line on what real clinical use would require: local validation, a reader study, a regulatory path.

**During the notebook:** roam as the clinical helper (help people interpret outputs, not debug code), and collect 1–2 clinically wrong outputs for the read.

- **Take-homes (max 3):** (1) Today VLMs are assistants, and the radiologist signs. (2) Fine-tune for behavior and local skill; prompt or retrieve for knowledge. (3) Judge a model with task-matched metrics and a radiologist's eye, not with how fluent it sounds.
- **Deliverable:** `Slides_1_Clinical_Context.pdf`, 8 or fewer content slides plus backup, including the checklist slide.
- **Suggested hand-off to Ali:** "So that's why and when. Ali, what actually changes inside the model when we fine-tune it?"
- **Cut first:** keep only one landscape example; shrink the read to a single case. **Never cut:** the automation-bias line.
- **Starting sources** (optional; verify before citing):
  - Flamingo-CXR (Nature Medicine, 2024)
  - Northwestern generative report drafting (JAMA Network Open, 2025)
  - Dratsch et al., automation bias (Radiology, 2023)
  - Yang et al., fairness and generalization (Nature Medicine, 2024)
  - ReXVal / RadEvalX for radiologist-annotated report errors

### 4.3 Ali: VLM and fine-tuning concepts (10 min)

- **Goal:** give the room a working mental model of a VLM's parts and of what fine-tuning changes, so that every object in Kalina's notebook maps to something on these slides.
- **LOs owned:** **LO1** (primary), **LO2** (primary); the mechanism side of LO5.

**MUST cover**
1. **VLM vs CNN vs LLM** (about 1 min): a CNN outputs fixed labels; an LLM reads only text; a VLM writes text conditioned on an image, which makes it flexible and also able to hallucinate.
2. **Anatomy** (about 2 min): vision encoder → projector/connector → language model, plus tokenizer and chat template. How an image becomes tokens, and why image resolution drives memory and speed. **Use the exact module names from Kalina's "inspect model" cell**, so the slide and notebook match.
3. **Training objective** (about 1 min): next-token prediction, and grading only the answer tokens, not the question (loss masking).
4. **Strategy table** (about 3 min): what's frozen or trained, memory, data needed and clinical fit for full fine-tuning, LoRA, QLoRA and prompt tuning. One line on prompt *engineering* (no training) vs prompt *tuning*. One line on which parts are frozen in our notebook.
5. **Knobs and failure modes** (about 2 min): learning rate, steps/epochs and LoRA rank; why overfitting and catastrophic forgetting happen; hallucination as the language prior overriding the image. Use the same knobs Kalina exposes in the notebook.

- **NICE (backup):** memory arithmetic (why full fine-tuning doesn't fit a T4); target modules; one adapter per task or site; DoRA and preference tuning (DPO/GRPO) in one line each; medically pretrained models (e.g. MedGemma) as a comparison.
- **OUT:** attention maths, RoPE, tokenizer algorithms, contrastive pretraining (Labs 03 and 06); clinical consequences (Julie); code (Kalina).
- **Take-homes (max 3):** (1) A VLM is a vision encoder plus a projector plus a language model; images become tokens. (2) LoRA/QLoRA trains about 1% or less of the weights as a small, removable adapter, which is the default when data and GPU are limited. (3) Overfitting and forgetting follow from learning rate, steps and data size: watch validation loss and check that the model's original skills survive.
- **Format (D6):** recommend PDF slides rather than a notebook. They work without GPU or WiFi, the director prefers PDF, and the live view of the model's parts is already in Kalina's inspect cell.
- **Deliverable:** `Slides_2_VLM_Fine_Tuning_Concepts.pdf`, 10 or fewer content slides plus backup.
- **Suggested hand-off to Kalina:** "Everything on these slides is a line in Kalina's notebook. If your setup isn't finished, switch to skip-training mode. Kalina?"
- **Cut first:** merge "image → tokens" into the anatomy slide. **Never cut:** the strategy table (LO2).

### 4.4 Kalina: hands-on notebook (18 min plus 5 min overflow)

- **Goal:** participants fine-tune a VLM on a radiology task themselves, then measure whether it improved and where it still fails.
- **LOs owned:** **LO4** (primary), **LO5** (primary); LO2 and LO3 in practice.

**MUST cover** (sequence and timing are Kalina's call; suggested split in brackets)
1. **Setup cell (run at 8:03, during the talks):** install, GPU check, download data and model, load the precomputed adapter. It prints a clear "SETUP COMPLETE".
2. **Inspect the model** [~2 min]: a short table of the components (frozen vs trained, parameter counts) with the same labels as Ali's slides, and the trainable-parameter percentage.
3. **Data** [~3 min]: the chat/prompt format, with **one fill-in cell followed by its completed version**. Plus a quick look at composition: split sizes, image-level leakage check, and the label conventions (e.g. laterality).
4. **Zero-shot baseline** [~2 min] on the anchor images.
5. **Live fine-tune** [~4 min]: a **short, capped run** (a few minutes at most) so people watch the loss fall. Walk through the config objects while it trains. They map to Ali's slides: quantization config = QLoRA, LoRA config = LoRA, training config = hyperparameters.
6. **Before/after** [~3 min] on the same anchors, using the **precomputed full adapter**, plus the metrics agreed in D9.
7. **One probe per failure mode** [~3 min]:
   - hallucination: blank or swapped image;
   - forgetting: adapter on vs off on general prompts;
   - overfitting: precomputed train vs validation loss curves ("predict, then reveal").
8. **Hand-off** [~1 min]: before/after stays on screen for Julie.

- **NICE (overflow or homework):** a hyperparameter explorer (a Colab form that picks one of several precomputed runs and plots its curve and score; keeps the README's promise to "experiment with hyperparameter choices"); per-category breakdown; saving your own adapter.
- **OUT:** architecture theory (Ali); clinical interpretation and regulation (Julie); data sourcing (Lab 08); a full training run live (precompute it); report-generation metrics (mention only).
- **Take-homes (max 3):** (1) With QLoRA, a small VLM fine-tunes on a free GPU in minutes. (2) Always compare against the base model on a fixed held-out set, and check how much of the gain is just answer format. (3) Probe failures on purpose: a good score doesn't prove the model looked at the image.
- **Deliverables:**
  - `<name>.ipynb` (outputs cleared) and `<name>_with_outputs.ipynb` (executed, for anyone without a GPU), each with its own Open-in-Colab badge;
  - small precomputed files (eval IDs, outputs, loss logs) in the repo, under 5 MB;
  - adapter weights hosted on Hugging Face (D8);
  - a 6–8 min backup screen recording, linked rather than committed.
- **Suggested hand-off to Julie:** "Here are the before/after answers on our anchor images. Julie, would you trust them?"
- **Cut first:**
  1. people run the completed data cell instead of the fill-in;
  2. move the overflow activities to homework;
  3. shrink each probe to one precomputed example.
- **Never cut:** the live training run, before/after on the anchors, one example per failure mode.

---

## 5. Shared decisions to lock

Recommended defaults come from initial research (Appendix A). The **owner decides**, and the pilot (Oct 23) can overrule any of them.

| # | Decision | Owner | Lock by | Recommended default | Why |
|---|---|---|---|---|---|
| D1 | Running example (task + anchors) | Kalina + Julie | Mon Oct 26 | Short-answer radiology VQA (closed yes/no + short open answers). 5–6 anchors across CT/MRI/X-ray, including one case the base model gets wrong and the adapter fixes, one it still gets wrong, and one disputed label. Julie vets them. | Scorable in seconds on a T4. Honest framing: VQA is the building block behind drafting and triage, not how radiologists read. |
| D2 | Base model and stack | Kalina | Wed Oct 14 (provisional) / Mon Oct 26 (final) | `Qwen/Qwen3-VL-2B-Instruct`, 4-bit QLoRA, plain Hugging Face stack (transformers + PEFT + TRL + bitsandbytes). Ship **one** stack. Unsloth is a pilot-time alternative only. | Apache-2.0 and **ungated** (no HF token for participants); small enough for a free T4. Confirm fp16 stability in the pilot. |
| D3 | MedGemma | Ali | Wed Oct 14 | Backup slide only; not in the notebook | Gated (needs HF account, license click and token); Google's fine-tuning notebook targets bf16/A100; Gemma has fp16 overflow issues on T4. |
| D4 | Dataset | Kalina (Julie for labels) | Mon Oct 26 | **SLAKE, English questions only.** Plan B: VQA-RAD re-split by image. | SLAKE's English splits share no images and are tagged by modality and question type. VQA-RAD test images reappear in its training split and in common VLM training mixes (a good LO3 teaching example). Licence check: Q3. |
| D5 | Terminology | Ali | Wed Oct 14 | "VLM" everywhere | Matches the retitle |
| D6 | Ali's format | Ali | Wed Oct 14 | PDF slides | See 4.3 |
| D7 | Run modes | Kalina | Fri Oct 30 | Three modes, no code edits: **GPU live** (default); **skip training** (checkbox; loads precomputed results); **no GPU** (replays saved outputs). | Live training keeps LO4 honest; nobody gets stuck. |
| D8 | Hosting adapter and artifacts | Ali (with director) | Fri Oct 16 | An organization-owned Hugging Face repo (RSNA or HOPPR), pinned by revision | Last year's artifacts sat on personal accounts, and links rot. |
| D9 | Eval set and metrics | Kalina; Julie signs off | Fri Oct 30 | A fixed held-out set (~200 questions). Closed accuracy plus sensitivity/specificity on abnormality questions; exact match for short answers (laterality: exact match only); majority-class and blank-image baselines; breakdown by modality. | Matches Julie's metric slide; separates gains in answer format from gains in visual skill. |
| D10 | File names and slide style | Ali | Fri Oct 30 | Names as in section 4; 16:9; ≥24 pt body; citations in footer | Badges and QR codes depend on file names |

**Pilot go/no-go (Kalina reports Oct 23; decide Oct 26).** Run on 2–3 fresh **free** Colab accounts:
- the Setup cell finishes in about 8 min or less;
- the live run finishes in about 2–3 min or less;
- peak VRAM leaves headroom;
- the full adapter clearly beats zero-shot on the eval set;
- at least half the anchors change visibly.

If it fails, try in order: fewer steps or smaller images → Unsloth on the same model → Plan B dataset.

---

## 6. Learning-objective coverage

P = primary · S = supporting · R = reinforced

| Learning objective | Julie | Ali | Kalina | Julie (read) | Wrap-up |
|---|---|---|---|---|---|
| LO1 What LVLMs are; how they differ from vision-only/text-only AI | S | **P** | R (inspect cell) | | R |
| LO2 Full FT, LoRA, prompt tuning; when each fits | S (when to fine-tune) | **P** | S (config objects) | | R |
| LO3 Data curation, annotation quality, composition | **P** | S | S (composition cell) | R | |
| LO4 Hands-on fine-tune in the cloud | | | **P** | | |
| LO5 Metrics; hallucination, forgetting, overfitting | S (metrics, error types) | S (why) | **P** (metrics, probes) | **P** (checklist) | R |

**README promises and where we deliver them**

| README promise | Delivered by |
|---|---|
| Dataset preparation and annotation best practices | Julie's data block; Kalina's composition cell; Lab 08 for engineering |
| Parameter-efficient training | Ali's strategy table; Kalina's QLoRA run |
| Experiment with hyperparameter choices | Kalina's "predict, then reveal" curves plus the explorer (overflow) |
| Report generation, VQA, findings classification | VQA live; findings classification = closed abnormality questions; report generation in Julie's landscape |
| Evaluation and failure analysis | Kalina's metrics and probes; Julie's read |
| No advanced programming required | One Setup cell, completed cells, forms and checkboxes, three run modes |

---

## 7. Notebook requirements checklist

From the director's email and `CONTRIBUTING.md`. **Owner:** Kalina. Ali checks it at each dry run.

- [ ] GPU need and expected time stated at the top; notebook metadata set to T4.
- [ ] **Disconnect and delete runtime → Run all** passes on a non-author **free** account, in all three run modes (D7).
- [ ] The Setup cell needs no runtime restart (no pins that downgrade Colab's preinstalled packages and force one).
- [ ] **Pinned versions** for every install. Model, dataset and adapter pinned by revision. A cell prints versions.
- [ ] Every fill-in cell is followed by its **completed version**.
- [ ] A markdown cell before each code cell says what it does and roughly how long it takes. The focus is the logic, not the syntax.
- [ ] Slow steps precomputed (full training, full evaluation, hyperparameter runs) by code in the repo with a fixed seed.
- [ ] **No secrets**, and no token needed on the default path. If a token is ever needed, use Colab Secrets and add it to the README.
- [ ] **Public data only**, downloaded at run time; credits cell for dataset and model licences; no PHI.
- [ ] No file over 100 MB; notebook under about 5 MB; no embedded base64 images.
- [ ] Strip `metadata.widgets` before committing (last year's notebook showed "Invalid Notebook" on GitHub because of it).
- [ ] Open-in-Colab badges point to `RSNA/AI-Deep-Learning-Lab-2026/blob/main/...`, not to a fork (Colab's "Save a copy in GitHub" writes the fork into the link).

---

## 8. Preparation timeline

| Date (2026) | Milestone | Owner |
|---|---|---|
| **Fri Oct 9** | Team call: agree this curriculum, D5/D6, the pilot thresholds, and who owns the fork. Check the README and the banner/program listing (names, credentials, VLM title). Send the director questions Q1–Q5. | All; Ali |
| Tue Oct 13 | **PR #1 (README only):** "Before the Session" pre-reqs and related labs, merged before social posts start in mid-October | Ali |
| Wed Oct 14 | Provisional D2; lock D3, D5, D6 | Kalina, Ali |
| Fri Oct 16 | Director answers due (hosting, licences, disclosures, helpers, AV) | Ali |
| **Fri Oct 23** | **Pilot** on free accounts. Kalina sends Ali the model's module names, and Julie 10–12 candidate anchors with outputs. | Kalina |
| **Mon Oct 26** | **Go/no-go.** Lock D1, D2, D4. Julie picks the anchors. | Kalina, Julie, Ali |
| Fri Oct 30 | **Draft 1** of all slides; notebook runs end-to-end in all modes. Lock D7, D9, D10. | All |
| **Tue Nov 3** | **Dry run 1:** full 45 min with a timer and a novice volunteer running the notebook | All (Ali times) |
| Fri Nov 6 | Freeze package versions against the current Colab runtime | Kalina |
| Sun Nov 8 | Final precompute on the frozen versions; adapter pushed to Hugging Face | Kalina |
| Mon Nov 9 | **PR #2:** notebooks, executed copy, slide PDFs, README Materials and Agenda tables (from a fork synced with upstream) | Ali, Kalina |
| Wed Nov 11 | **Dry run 2** from the PR branch on fresh free accounts; contingency drill (no GPU, WiFi off); record the backup video | All |
| Fri Nov 13 | Target merge (regulatory line re-checked) | Ali; Julie |
| **Sun Nov 15** | **Merge deadline and content freeze** | All |
| Nov 16–22 | Director test-runs the notebook; fix flagged items in one batched PR | Kalina, owners |
| **Tue Nov 24** | **Final rehearsal** and a smoke test from the RSNA `main` badge | All |
| Thu Nov 26 | US Thanksgiving | none |
| Tue Dec 1 | Re-check the notebook (read-only); visit the room and test AV if possible | Ali, Kalina |
| **Wed Dec 2** | **Lab day.** Faculty arrive about 7:15. | All |

---

## 9. Day-of roles and contingencies

**Before doors**
- ~7:30: Kalina warms up her own runtime (and a backup on a second account) and runs the Setup cell.
- Ali sets up one presenter laptop with all slide PDFs in run order, plus the executed notebook and recording available offline.
- Setup slide on screen: QR code, short URL, four setup steps.
- Phone hotspot ready.

| Segment | Presents | Keeps time (front row) | Roams to help |
|---|---|---|---|
| Doors and kickoff | Ali | none | Julie, Kalina |
| Julie (context) | Julie | Ali | Kalina |
| Ali (concepts) | Ali | Julie | Kalina |
| Kalina (notebook and overflow) | Kalina | Ali | Julie (clinical), Ali when free |
| Julie (read) | Julie | Ali | none |
| Wrap-up and Q&A | Ali | Julie | none |

- **Helpers:** the director suggests a facilitator in addition to the presenter. Three faculty give us two roamers most of the time. An extra helper is welcome for 30–40 people (Q1). Help the back rows first, never take over the keyboard, and send anyone more than about 2 cells behind to the completed cells or skip-training mode.
- **Time signals:** a countdown visible from the stage, plus "2 min" and "STOP" cards. On STOP, finish the sentence and hand off.
- **Questions:** setup problems are handled one-to-one by roamers. Concept questions go to the parking lot and are answered at 8:53.

| If… | Then… | Who decides |
|---|---|---|
| A participant has no GPU | No-GPU mode replays saved outputs automatically | Roamer |
| A participant is behind at 8:24 | Tick "skip training"; everything else runs | Participant, with roamer |
| More than half the room isn't set up at 8:20 | Presenter-only mode: Kalina drives; the room follows the executed copy | Ali |
| Venue WiFi is down | Hotspot; local PDFs; backup recording | Ali |
| Colab update breaks the install after the freeze | Backup runtime → skip-training → no-GPU mode → executed copy. No last-minute code changes. | Kalina |
| Running late | Apply each segment's "cut first" list. The overflow absorbs the notebook. Q&A shrinks, but 8:58 holds. | Timekeeper |

**Never cut:** setup instructions at kickoff, live training, before/after on the anchors, one example per failure mode, the take-home slide, the 8:58 stop.

---

## 10. README updates

**PR #1 (by Oct 13), "Before the Session":**
- keep laptop + Chrome + Google account;
- add "use a **personal** Google account (hospital and work accounts often block Colab)";
- add "have your phone for sign-in verification";
- add "avoid heavy Colab GPU use in the 24 h before the lab (free GPU quota is limited; the notebook still runs without a GPU)";
- add "no Hugging Face account needed" (only if D2/D3 hold);
- add a "Related labs" line: Lab 03, Lab 04, Lab 06, Lab 08.

**PR #2 (by Nov 9):**
- a Materials table: notebook badge, executed copy, three slide PDFs, adapter link;
- a short Agenda table (time · segment · presenter).

**Lab 08 cross-reference:** Julie's data block, Kalina's data cell and Ali's wrap-up each say: "Building de-identified image-report pairs from your own data is Lab 08, at 9:30 today."

---

## 11. Open questions

| # | Question | Owner | By | Default if no answer |
|---|---|---|---|---|
| Q1 | Does RSNA provide room helpers? Do we bring an extra facilitator? | Ali → director | Oct 16 | Three faculty roam in rotation |
| Q2 | Room access time, screens, mics, seat power, network | Ali → director | Oct 16 | Arrive 7:15; bring a hotspot |
| Q3 | Dataset licence is acceptable (SLAKE is CC BY 4.0, but some upstream images are CC BY-NC-SA)? Licence for our adapter? | Ali → director | Oct 16 | Use SLAKE, list all upstream licences, research/education use |
| Q4 | RSNA disclosure wording, and who shows it | Ali → director | Oct 16 | Disclosure slide in Ali's kickoff |
| Q5 | Hosting org for the adapter (D8) | Ali → director | Oct 16 | HOPPR org on Hugging Face |
| Q6 | Who owns the fork and opens PRs? | Team | Oct 9 | Ali's fork, with Julie and Kalina as collaborators |
| Q7 | Does this curriculum go in the upstream PR? | Team | Oct 9 | No. The README gets an Agenda table instead. |
| Q8 | Should we ask the Lab 08 faculty to mention us too? | Ali | Oct 30 | Yes |

---

## Appendix A. Initial research notes (Oct 4, 2026; verify in the pilot)

Background behind the defaults in section 5. Owners should re-check anything they rely on.

**Precedent (RSNA 2025 fine-tuning lab)**
- It was text-only: Llama-3.1-8B with LoRA via Unsloth.
- Good: an "estimated time" banner on each step, and the same test case shown before and after fine-tuning.
- Problems:
  - it claimed "free T4" but outputs came from an A100;
  - partial version pins;
  - evaluation and model lived on personal accounts;
  - committed the day before the lab, then failed to render on GitHub because of widget metadata.
- 2025 lab: [RSNA/AI-Deep-Learning-Lab-2025](https://github.com/RSNA/AI-Deep-Learning-Lab-2025).

**Models (Hugging Face, checked Oct 4)**

| Model | Licence | Gated | Notes |
|---|---|---|---|
| [Qwen3-VL-2B-Instruct](https://huggingface.co/Qwen/Qwen3-VL-2B-Instruct) | Apache-2.0 | No | ~4.3 GB download; trained in bf16, so use fp16 compute on T4 with care; a 512×512 image ≈ 256 visual tokens. TRL has an official [Qwen3-VL QLoRA notebook](https://github.com/huggingface/trl/blob/main/examples/sft_qwen3_vl/sft_qwen3_vl.ipynb) aimed at free-tier T4. |
| [MedGemma 1.5 4B](https://huggingface.co/google/medgemma-1.5-4b-it) | HAI-DEF terms | Yes | Medically pretrained (and trained on SLAKE, so not a fair comparison on it). Google's [fine-tuning notebook](https://github.com/google-health/medgemma/blob/main/notebooks/fine_tune_with_hugging_face.ipynb) needs bf16/A100; on T4 only Unsloth's fp16 path is known to work. |
| Gemma 4 E2B | Apache-2.0 | No | Backup via [Unsloth](https://unsloth.ai/docs/models/gemma-4/train); ~10 GB download; Gemma models overflow in plain fp16. |
| Qwen2.5-VL-3B | qwen-research (non-commercial) | No | Avoid (licence; fp16 issues reported on T4). |

**Colab**
- Free-tier GPUs are [not guaranteed](https://research.google.com/colaboratory/faq.html).
- The runtime changed twice in Sep 2026 (Ubuntu 24.04, CUDA 13); see [backend-info](https://github.com/googlecolab/backend-info). Expect another update before Dec 2, hence the Nov 6 freeze and the Nov 24 smoke test.
- transformers v5 renamed APIs (`AutoModelForVision2Seq` → `AutoModelForImageTextToText`, `torch_dtype` → `dtype`), so 2025-era code breaks.
- No FlashAttention 2 on T4 (use SDPA).
- Model downloads run on Google's network, not the venue WiFi.

**Datasets**
- [SLAKE](https://huggingface.co/datasets/BoKelvin/SLAKE):
  - English splits are 4,919 / 1,053 / 1,061 QAs on 450 / 96 / 96 images, with no shared images;
  - questions are templated (most test question strings also appear in training), so part of any gain is format;
  - don't mix in the Chinese questions (they share images with the English test set);
  - some position labels follow a viewer-side convention, a good LO3 example.
- [VQA-RAD](https://huggingface.co/datasets/flaviagiammarino/vqa-rad):
  - CC0;
  - 202 of 203 test images also appear in its training split, and that split is in common VLM training mixes;
  - use only as a leakage example or Plan B.
- Avoid for walk-in participants: MIMIC-CXR (credentialed); CheXpert and PadChest (restricted, no redistribution); MedPix re-uploads (unclear licence); ROCOv2 (18.6 GB).

**Clinical (for Julie to verify)**
- Regulatory status: as of mid-2026 research, no FDA-authorized device generates radiology report text. A few chest X-ray drafting tools hold Breakthrough designation, which isn't clearance. Re-check in November.
- Report-error taxonomies and metrics:
  - [ReXVal](https://physionet.org/content/rexval-dataset/)
  - [GREEN](https://arxiv.org/abs/2405.03595)
  - [TRIPOD-LLM](https://pubmed.ncbi.nlm.nih.gov/39779929/)
