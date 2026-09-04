# Using Claude in the CERG-FLUX Lab

**A practical guide for postgraduates, postdocs and collaborators**

CERG-FLUX Lab (Fluids, Learning, and Uncertainty in compleX systems)
Department of Mechanical and Aeronautical Engineering, University of Pretoria

---

## How to read this

- **Section 1–2** are compulsory. Read them before your first session.
- **Section 3** gets you set up in about fifteen minutes.
- **Section 4** is the how-to: prompting habits, copy-paste recipes for common Lab tasks, and how a good session runs.
- **Sections 5–10** are the tool-by-tool reference. Skim now, return when relevant.
- **Section 11** is the checklist to come back to every few months.

If you read nothing else, read **§2 (Ground rules)** and **§11 (Red flags)**.

---

## 1. What Claude is for in this Lab

Claude is an accelerator for the parts of research that are *not* the research: the boilerplate, the scaffolding, the formatting, the admin, the second pair of eyes. It is not a substitute for thinking, and it is not a co-author.

The Lab's position on this is set out formally in the **AI Research Guardrails**:

> https://github.com/cerg-flux-lab/ai-research-guardrails

That document is the governing framework. This guide is the *operational* companion to it — how to actually use the tool well, within those limits.

**The single sentence version:** AI is an amplifier, never the origin.

---

## 2. Ground rules

### 2.1 Institutional (non-negotiable)

| Rule | What it means in practice |
|---|---|
| **Academic use only** | These seats are for CERG-FLUX research and teaching. Consulting, paid external projects and commercial CPD go on a separate personal account. |
| **Lab members and active collaborators only** | Do not share your seat or paste a colleague's work in on their behalf without their knowledge. |
| **POPIA and UP data governance** | No restricted, personal or third-party confidential data in the workspace unless UP policy *and* your ethics clearance explicitly permit it. This includes student records, unpublished collaborator data, and anything under NDA. |
| **UP policy supersedes everything here** | Acceptable use of IT, research ethics and integrity, information governance. If this guide and a UP policy conflict, the policy wins. |
| **Usage credits are off** | You will be throttled at your limit, not billed extra. Pace yourself — don't burn a day's quota on a task you could have done in your head. |

### 2.2 The three-tier framework (from the Guardrails)

| Tier | Applies to | Claude may | Claude may not |
|---|---|---|---|
| **Tier 1 — My mind, my voice** | Thesis, manuscripts, literature review, conference arguments, lecture content, scientific logic in code (loss functions, boundary conditions, architecture rationale, physical reasoning), methodology sections of READMEs | Explain concepts, suggest directions, flag errors, check references, format text, ask probing questions | Draft prose, structure arguments, write explanatory content, make research design decisions |
| **Tier 2 — My direction, Claude's drafting** | Professional emails, formal correspondence, LinkedIn posts, admin communications, grant boilerplate | Produce a draft from your direction, context, tone and key points | — (test: *you could have written it yourself; Claude saved time, not thought*) |
| **Tier 3 — My specification, Claude's execution** | Websites, scrapers, automation scripts, infrastructure, build systems, plotting utilities, CI/CD, Beamer templates | Implement to your specification. You approve the result | — |

### 2.3 The viva test

If you cannot independently defend a piece of work — the reasoning, the design choices, the arguments — **without referring to a conversation history**, then AI did too much.

For postgraduates this test is literal. You will sit in a room and defend this. "Claude suggested it" is not an answer to "why this boundary condition?"

---

## 3. Getting set up (do this first)

1. **Read the Guardrails repo** end to end. Ten minutes.
2. **Set your user preferences.** Settings → Profile. Tell Claude how you want it to respond — response length, whether you want SI units, British vs American spelling (we use **British/South African English**: *modelling*, *analyse*, *behaviour*), whether you want it to push back rather than agree. This applies to every new conversation and saves you repeating yourself.
3. **Turn on the features you want.** In-conversation settings control web search, extended research, code execution and file creation, artifacts, and searching your past chats. Most people should have search and file creation on.
4. **Create your first Project** (see §5).
5. **Clone the guardrails repo** next to your project repos if you use Claude Code:
   ```
   git clone git@github.com:cerg-flux-lab/ai-research-guardrails.git
   ```
6. **Join the Lab Discord** and post questions in **#general** — if you find a prompt pattern that works well, share it there so the rest of the Lab benefits.

---

## 4. How to actually use it

### 4.1 Prompting habits

Most disappointing outputs are underspecified prompts. Five habits fix ninety percent of it.

**1. Give context, not just an instruction.**

> ✗ "Explain the Chapman–Enskog expansion."
>
> ✓ "I'm a first-year MEng student working on an LBM solver for conjugate heat transfer. I understand the BGK collision operator but I don't see how the Chapman–Enskog expansion recovers Navier–Stokes. Walk me through it at the level of a graduate fluid mechanics course, and stop and check my understanding at each step."

**2. Say what the output is for and what shape it should take.**

Specify the audience, the length, the format, and the destination. "A 200-word abstract for a CFD conference, no citations" beats "write me an abstract.". 

**Test Question, "based on the gaurdrails, should Claude draft an abstract?"**

**3. Use examples.** Paste one figure caption you like, then ask for five more in that style. Positive and negative examples both help — "not like this: [example]" is a legitimate instruction.

**4. Ask for reasoning before the answer** on anything technical. "Work through this step by step before you give me the final expression." Claude will think harder if you ask it to.

**5. Iterate rather than restart.** Give targeted corrections — "keep everything, but the third paragraph is too promotional and the units in Table 2 should be W/m·K" — rather than re-prompting from scratch. You will get better results and use less quota.

**Also worth knowing:**

- **Ask Claude to critique, not to produce.** "Here is my argument for why the AQT cooling model needs a two-phase treatment. Find the three weakest links." This is Tier 1–safe and often the highest-value use of the tool.
- **Ask it to interrogate you.** "Ask me questions until you understand my research problem well enough to explain it back." Excellent for clarifying your own thinking before you write.
- **Tell it when it's wrong.** It is not always right, and it will fold too easily if you push without cause. Push only when you have a reason.
- **Claude hallucinates citations.** It has no live bibliographic database unless you give it one. Every reference it produces must be verified against the actual paper. Use the PubMed/bioRxiv/Consensus connectors (§7) rather than trusting recall. **You still have to read these papers and not use Claude to summarise it with reading it and verifying the summaries against your understanding of the papers**

### 4.2 Recipes for common Lab tasks

Copy these, edit the brackets. Each is marked with its tier.

**Understanding a paper you're stuck on — Tier 1**

> I've attached [paper]. I'm stuck on [Section 3.2, the derivation of the effective relaxation time]. Do not summarise the paper. Instead: explain that section step by step, and after each step ask me a question to check I've followed. If I get one wrong, don't give me the answer — tell me what I've misunderstood and let me try again.

**Stress-testing your own reasoning — Tier 1, highest-value use of the tool**

> Here is my argument for [why the AQT cooling model needs a two-phase treatment]: [paste your argument]. Do not improve it. Act as a hostile examiner: find the three weakest links, tell me what a reviewer would attack first, and name the assumption I haven't justified.

**Clarifying a half-formed idea before you write — Tier 1**

> I have a rough idea for [a chapter arguing that mesh-independence studies in LBM papers are usually under-reported]. Ask me questions, one at a time, until you understand it well enough to explain it back to me. Don't offer suggestions until I say stop.

**Literature scoping — Tier 1, with connectors on**

> Using the Consensus and PubMed connectors, find work published since [2020] on [physics-informed neural networks for compressible flow with shocks]. For each: title, authors, year, DOI, and one sentence on what they actually did. Only include papers you have retrieved through a connector — if you cannot verify it exists, leave it out. Do not tell me what the gap in the literature is; I'll decide that.

**Debugging — Tier 3**

> Here's the error and the traceback: [paste]. Relevant file attached. Before you propose a fix, tell me what you think is happening and how confident you are. Then give the smallest change that would fix it.

**Implementation to spec — Tier 3**

> Write a plotting utility that takes [a directory of VTK output files] and produces [a 2×2 panel figure of velocity magnitude at four timesteps], styled for [a two-column journal, 8.6 cm wide, serif labels, colourblind-safe map]. Python, matplotlib, no seaborn. Just the utility — the physics is already handled upstream.

**Professional email — Tier 2**

> Draft an email to [a collaborator at CERN] explaining that [our thermal FEA results are delayed by three weeks because the licence renewal is stuck in procurement]. Tone: apologetic but not grovelling, factual, offers a concrete new date of [12 October]. Six sentences maximum. I'll edit before sending.

**Preparing for a supervision meeting — Tier 1**

> I'm meeting my supervisor on Thursday about [progress on Chapter 4]. Here's where things stand: [paste]. Ask me the five hardest questions they're likely to ask, one at a time. Wait for my answer before the next one.

**Reviewer response — Tier 1 substance, Tier 2 wording**

> Reviewer 2's comment: [paste]. My position is: [I disagree, because the reviewer has assumed a Boussinesq approximation we explicitly stated we don't use]. Help me phrase that as a polite, firm response. Do not soften my position or concede the point — just make the language appropriate for a journal.

**Formatting and LaTeX — Tier 3**

> Convert this table into a `booktabs` LaTeX table for a two-column layout, with units in the header row and a caption placeholder. Don't change any numbers.

### 4.3 How a good session runs

1. **Start in the right place.** The relevant Project, or Claude Code inside the repo. Not a blank chat.
2. **Front-load the context.** Attach the files, state your level, state the constraint, state the tier if it's ambiguous.
3. **Ask for a plan before output** on anything substantial. *"Don't write it yet — tell me your approach."* Cheap to correct at this stage, expensive later.
4. **Work in passes.** One thing at a time, corrected, then the next. Long unbroken generations are where errors hide.
5. **Interrogate anything that surprises you.** *"Why that and not [alternative]? What would break if I did it the other way?"* If the answer is thin, the output is thin.
6. **Verify before it leaves the chat.** Citations against real sources. Numbers against your own calculation. Code by running it.
7. **Start a fresh conversation when you change task.** Context from an unrelated problem degrades the answer and burns quota.

### 4.4 When not to use it

- When you're avoiding thinking. The urge to open a chat instead of a notebook is usually a signal that the problem is hard and you don't want to start. Start anyway.
- When the answer needs to be *yours* and you're tired enough to accept whatever comes back. Come back to it tomorrow.
- For anything containing restricted, personal or third-party confidential data (§2.1).
- For a task you can finish in two minutes yourself. Quota is finite.
- As a search engine for facts you'll use without checking. Use a connector, or check the source.

---

## 5. Projects — use them

A **Project** is a persistent workspace with its own uploaded files, its own instructions, and its own memory. This is the single most under-used feature in the Lab.

### Setting one up

1. Open **Projects** in the left sidebar of Claude, then **Create project**.
2. Name it after the research thread, not the task — `MEng — LBM conjugate heat transfer`, not `thesis chapter 3`.
3. **Add project instructions.** This is the important part; see the template below.
4. **Add files to project knowledge.** Upload the things you'd otherwise re-explain every time: your thesis outline, the solver README, the three papers your work builds on, your supervisor's last feedback memo, your notation conventions.
5. Start every conversation on that thread *inside* the Project. Conversations started outside it get none of the above.

### Project instructions template

Copy this, edit the bracketed parts:

```
I am [a second-year MEng student] in the CERG-FLUX Lab, University of Pretoria,
working on [lattice Boltzmann simulation of conjugate heat transfer in
electronics cooling].

Context you should assume:
- My background is [mechanical engineering; strong on continuum fluid mechanics,
  weaker on statistical mechanics and C++ templates].
- Notation: [I use tau for relaxation time, not omega. SI units throughout.]
- Language: British/South African English. Never American spelling.

How I want you to work with me:
- This project is Tier 1 under the CERG-FLUX AI Research Guardrails. Do NOT
  draft thesis prose, literature review text, or research arguments for me.
- When I ask about physics or method choices, engage Socratically — ask me
  questions, point out what I've missed, stress-test my reasoning. Do not hand
  me conclusions.
- You may freely help with: debugging, plotting utilities, LaTeX formatting,
  build scripts, and checking my citations against real sources.
- Never invent a citation. If you are not certain a reference exists, say so
  and use a connector to check.
- Be direct. If I am wrong, say so plainly and say why.
```

### Suggested Projects

Set one up per research thread, not per conversation. For example:

- `MEng — LBM conjugate heat transfer` — with your thesis outline, key papers, solver README, and supervisor feedback uploaded.
- `ATLAS ITk AQT thermofluids` — with the relevant technical notes and the collaboration's naming conventions.
- `MKM411 teaching` — with the study guide and assessment rubrics.

**Project memory is scoped to the Project.** What Claude learns in your teaching Project doesn't leak into your thesis Project. Use this deliberately.

**Note:** uploaded project files are subject to the same POPIA rules as everything else.

---

## 6. Skills and plugins

**Skills** are reusable instruction sets that make Claude follow the Lab's conventions without you re-explaining them. The Lab already has several:

| Skill | Triggers on |
|---|---|
| `up-formal-documents` | Letters, memos, motivations to HoD/Dean/committees, formal UP correspondence — encodes letterhead, signature block, titles, colours |
| `postgrad-supervision` | Motivations to the Postgraduate Studies Committee, progress reports, examiner nominations |
| `lab-paper-style` | Journal and conference manuscripts, arXiv preprints, LaTeX/Overleaf work, reviewer responses, abstracts |
| `teaching-pack` | MIA 320 and MKM411 materials — study guides, slides, assessments, notebooks |

You do not need to invoke these by name. Describing the task is enough: *"draft a motivation for a co-supervisor appointment for [student]"* will pull in `postgrad-supervision` automatically.

**If you find yourself pasting the same context into Claude for the third time, that's a skill.** Flag it to Muaaz and it can be added to the Lab catalogue so everyone benefits.

---

## 7. Connectors — stop working from memory

Connectors give Claude live access to external sources. The workspace currently has:

| Connector | Use it for |
|---|---|
| **PubMed** | Biomedical and life-sciences literature |
| **bioRxiv** | Preprints |
| **Consensus** | Evidence synthesis across papers — good for "what does the literature actually say about X" |
| **Clinical Trials**, **ChEMBL** | Trials and chemistry data (relevant to collaborators more than core Lab work) |
| **Google Drive** | Pulling in your own documents |
| **Claude in Chrome** | Browsing and acting on web pages — useful for portals, forms, and sites without an API |

**Why this matters:** a literature question answered from a connector is verifiable. The same question answered from the model's memory may be fluent and wrong. For anything going into a thesis or manuscript, use a connector or web search and then **check the source yourself**.

**Guardrails note:** a connector-assisted literature search is Tier 1 territory. Claude may surface papers. You read them, you decide what's relevant, you write the review.

---

## 8. Claude Code — for anyone with a research repo

If you write solver code, analysis pipelines or simulation tooling, Claude Code is worth the setup. It runs from the terminal, VS Code, JetBrains, or the desktop app and works directly on your repository.

**Docs:** https://docs.claude.com/en/docs/claude-code/overview

### Installing it

You need **Node.js 22 or newer**. Check with `node --version`; if you're below 22, install a current version first (`nvm install 22` is the least painful route on Linux and macOS).

```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

Then, from inside a repository:

```bash
cd ~/research/lbm-conjugate-ht
claude
```

The first run will prompt you to sign in — use the same account as your Lab workspace seat. If you prefer an IDE, there are VS Code and JetBrains integrations; the desktop app also has a Code tab.

### First session in a repo

1. Run `claude` in the repo root.
2. Ask it to orient itself before you ask for anything: *"Read the repository and tell me what it does, how it's structured, and what you're unsure about."* Correct its misunderstandings now — they'll propagate otherwise.
3. Run `/init` to generate a starting `CLAUDE.md`, then **rewrite it** according to the Lab configuration below. The generated version will not know about the Guardrails or which files are Tier 1.
4. Work in small, reviewable steps. Ask for a plan before it edits anything: *"Don't write code yet. Tell me how you'd approach this and which files you'd touch."*
5. Commit often, and read every diff before you commit. If you can't explain a hunk, don't commit it.

Useful in-session commands: `/init` (scaffold `CLAUDE.md`), `/clear` (reset context when you switch tasks — cheaper and more accurate than letting a long session drift), `/model` (switch models), `/help`.

### The Lab's mandatory configuration

Every research repository must have a `CLAUDE.md` at its root, and the **first line** must import the guardrails:

```markdown
@ /path/to/ai-research-guardrails/README.md

# Project: [name]

## What this repo is
[one paragraph — you write this]

## Scientific logic — Tier 1, do not modify without discussion
- src/collision.py — BGK operator, relaxation time derivation
- src/bc/ — boundary condition implementations and their physical justification

## Implementation — Tier 3, free to modify to spec
- scripts/, plotting/, ci/
```

Clone the guardrails repo alongside your project repos so the relative path resolves. This loads the framework at the start of every session, so Claude knows which parts of your codebase it must not think for you.

### Commit and attribution policy

- **Never** use `Co-Authored-By:` trailers for AI tools. Co-authorship implies shared intellectual contribution and shared IP. AI tools have neither, and the ambiguity creates real problems for NRF rating claims, journal submissions, UP IP policy compliance, and degree conferral.
- **Do** include an Attribution section in your README. Template:

```markdown
## Attribution

AI tools were used in the development of this repository:

- **Claude (Anthropic)** — debugging, code review, documentation formatting,
  implementation of plotting and build tooling.

All research design, scientific logic, physical reasoning, architecture decisions
and written outputs are authored solely by the project maintainers. All
intellectual property vests in the authors and the University of Pretoria.
```

- **Do not** list AI contributions as "architecture decisions" or "physics implementation guidance." Those are yours.

---

## 9. Beyond the chat window

Things the Lab is largely not using yet, roughly in order of payoff:

### Cowork — for multi-step work

Best for tasks that span many files and several tools: a literature sweep across thirty PDFs, restructuring a chapter's figures, cleaning a directory of simulation output, building a comparison table from a folder of results. A chat thread handles these badly; Cowork is built for them.

**Setup:**

1. Install the **Claude desktop app** and sign in with your Lab seat.
2. Open the **Cowork** tab.
3. Point it at a folder and describe the outcome you want, not the steps: *"This folder has 34 PDFs of LBM papers. For each one, pull out the collision operator used, the lattice (D2Q9/D3Q19/etc.), the Reynolds number range tested, and whether they treat conjugate heat transfer. Give me a spreadsheet."*
4. Let it run, then check its work. It can also be reached from the Claude mobile app if you want to start something and walk away.

**Guardrails note:** the extraction above is Tier 3 — Claude is doing clerical work to your specification. Deciding which of those 34 papers matter, and what the gap in the literature is, remains Tier 1 and yours.

### Everything else

**Artifacts and file creation** — Claude can produce actual `.docx`, `.pptx`, `.xlsx` and `.pdf` files, not just text in a chat box. Useful for progress report templates, examiner nomination forms, and slide scaffolds. Ask for the file explicitly ("give me this as a Word document") or you'll get chat text.

**Claude in Excel / PowerPoint / Word** — works inside the application. Excel is genuinely good for cleaning experimental data and building parametric models. PowerPoint for turning an outline into a first-pass deck (then you rewrite the content — Tier 1).

**Claude Design** — canvas-based visual work. Relevant for conference posters, the Lab website, module infographics.

**Model selection** — Opus for hard reasoning and long technical work, Sonnet for everyday drafting and code, Haiku for fast simple tasks. Using Opus for a formatting job wastes quota.

**Search past chats** — Claude can retrieve your previous conversations. "What did we settle on for the mesh independence criterion last month?" works. Enable it in settings.

**AI-powered artifacts** — an artifact can itself call the Claude API. Useful for building small internal tools: a marking-rubric assistant, a reference-formatting checker.

**The API** — for programmatic work at scale: batch-processing a thousand abstracts, running a structured extraction over a corpus, or embedding a model call inside an analysis pipeline. Docs at https://docs.claude.com/en/api/overview. **Speak to Prof Muaaz Bhamjee before setting anything up on a Lab account** — API usage is billed separately from your workspace seat and keys must not be provisioned independently.

---

## 10. Worked examples — where the line falls

| Task | Tier | How to do it |
|---|---|---|
| Understanding a paper's derivation | 1 | "Explain this step. Then ask me to reproduce it." Never "summarise this paper for my lit review." |
| Writing your literature review | 1 | You write. Claude may check grammar, flag an unclear sentence, verify a citation format. |
| Choosing a loss function for a PINN | 1 | You decide, having read the literature. You may ask Claude to stress-test your rationale. |
| Deriving the rationale you'll defend in your viva | 1 | Yours entirely. If Claude wrote it, you can't defend it. |
| Debugging a segfault in your solver | 3 | Paste the trace, let it work. |
| Writing the training loop scaffolding | 3 | Specify, let it implement, read and approve the result. |
| A README methodology section | 1 | You write it. Claude formats at most. |
| A README installation section | 3 | Let it draft. |
| Email to a collaborator about a delayed dataset | 2 | Give it the context and tone, edit, send in your own voice. |
| A conference abstract | 1 | You write. Claude may tighten wording once your argument is fixed. |
| Beamer template, plotting utilities, CI config | 3 | Free rein to specification. |
| Reviewer response letter | 1 for the substance, 2 for the wrapping | You decide what to concede and how to argue. Claude helps phrase it politely. |

---

## 11. Red flags and self-tests

Run these periodically.

- **The whiteboard test.** Can you explain a design choice to your supervisor without opening a chat history?
- **The cold-read test.** Open a file you haven't touched in two weeks. Can you explain every decision in it?
- **The removal test.** If you removed AI entirely, could you reproduce this work from your own understanding?

**Warning signs you've drifted:**

- You're copying output into your thesis and editing lightly rather than writing.
- You can't reconstruct why a parameter has the value it has.
- Your first move on a hard problem is to open a chat rather than a notebook.
- You'd be uncomfortable if your supervisor read the conversation history.
- You're asking Claude what your contribution is.

If any of these are true, stop and internalise the work before it carries your name.

---

## 12. Quick reference

```
BEFORE YOU START                      WHEN OUTPUT IS POOR
□ Is this Tier 1, 2 or 3?             □ Did I give context?
□ Any restricted/personal data?       □ Did I say who it's for?
□ Am I in the right Project?          □ Did I give an example?
□ Do I need a connector for this?     □ Did I ask for reasoning first?
                                      □ Am I iterating or restarting?

BEFORE IT CARRIES YOUR NAME           REPO HYGIENE
□ Can I defend this cold?             □ CLAUDE.md imports guardrails
□ Did I verify every citation?        □ No Co-Authored-By: AI trailers
□ Is the prose mine?                  □ Attribution section in README
□ Is the reasoning mine?              □ Tier 1 files marked
```

---

## Questions, gaps, improvements

This guide is a living document, like the Guardrails it sits under. If you find a gap, a better prompt pattern, or a case the tiers don't cleanly cover, raise it in **#general** on the Lab Discord, or with **Prof Muaaz Bhamjee** directly.

**Reminder:** this does not supersede University of Pretoria rules, regulations and policies.

---

*CERG-FLUX Lab · University of Pretoria*
*Built on the AI Research Guardrails (CC BY 4.0) — https://github.com/cerg-flux-lab/ai-research-guardrails*
