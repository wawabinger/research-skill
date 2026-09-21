---
name: paper-reading
description: Turn an academic paper (PDF or extracted text) into a structured bilingual (Chinese notes + English field labels) paper-reading note, following a fixed Abstract/Introduction/Method/Experiment/Limitation template. Use this whenever the user asks to "read", "精读", "summarize", "总结", or "做笔记" for a specific paper, wants "paper reading notes" or "论文笔记" produced from a PDF/arXiv link/local file, or says things like "帮我读一下这篇论文" or "把这篇 paper 整理成笔记". Also trigger when the user is building up a personal paper-reading corpus and asks to apply "the template" or "之前那个模版" to one or more new papers. Do NOT use this for improving the user's OWN paper draft (that's paper-writing help, a different task) — this skill is for reading and critiquing someone else's published paper.
---

# Paper Reading

## Why this template, and why it works

This template was reverse-engineered from a researcher's own hand-written reading notes
(`references/worked_example_original.md`). Its value is not the section headers — Abstract/Method/Experiment
are obvious — it's two structural constraints that force real understanding instead of summary paraphrase:

1. **Every Method module must answer four questions**: motivation / 做法 (what it does) / 为什么能work (why it
   works) / technical advantage. Skipping "为什么能work" is the single most common way a paper-reading note
   degrades into "restating the abstract in bullet form." A module description that only says what the module
   does, without explaining why that design choice is sound, has not actually been understood yet.
2. **Limitation is two separate tiers, never merged**: what the paper itself admits, and a separate
   "我（GPT）认为的" tier of independent critical judgment (error accumulation across pipeline stages,
   unstated threat-model assumptions, boundary conditions the authors didn't discuss). Merging these two
   collapses the note back into the paper's own narrative — the whole point of the second tier is to stop
   the paper's framing from being the last word.

Keep both constraints intact even under time pressure. A note that fills in every field but treats them as
boxes to check, rather than questions to actually answer from the paper's content, defeats the purpose.

## Workflow

1. **Get the paper's actual content, not just its abstract.** Read enough of the Introduction, Method, and
   Conclusion/Limitation/Discussion sections to fill every template field with real, specific content pulled
   from the paper — never placeholder text, never content invented to sound plausible. For a PDF, read it in
   page ranges (the Read tool caps at 20 pages per call); for a long paper, prioritize Abstract → Introduction
   → Method → Conclusion/Limitations, and only pull Experiment details deep enough to name the actual
   comparisons and ablations run (you don't need every table, just what was tested against what).
   If a plain-text extraction already exists (e.g. a sibling `.txt` next to the PDF), prefer reading that —
   it's cheaper than re-parsing PDF pages and gives you exact quotable phrasing for things like the paper's
   own stated contributions or limitations.
2. **Load `references/paper_reading_template.md`** for the exact structure and field names to fill in blank
   (Task/Technical challenge/Key insight/technical contribution under Abstract; Task and application/previous
   methods+limitation/Pipeline under Introduction; overview+per-module four-question breakdown under Method;
   comparison experiments/ablation study under Experiment; the two-tier Limitation).
3. **Calibrate depth and tone against the worked examples**, not against instinct: `references/worked_example_original.md`
   (the original hand-written note this template was extracted from) and `references/worked_example_trace.md`
   (a full note built by actually reading a paper's PDF/text end to end). Both are terse Chinese bullet notes
   that freely mix in English technical terms (module names, metric names, theorem references) rather than
   translating everything — match that register. Do not write full prose paragraphs; every line should be a
   bullet a researcher would actually jot down while reading, not a sentence written for a general audience.
4. **Write the note as a new markdown file.** Put the two guidance HTML comments (crop an appropriately-scoped
   figure — architecture/pipeline diagram, not a full-page screenshot — and add a one-sentence caption under
   it) at the very top of the file, before the title, exactly once — not repeated near the Method section's
   screenshot placeholder, which stays as a bare placeholder line.
5. **Ask for a save location and filename only if genuinely ambiguous** (e.g., the user hasn't named the
   paper or given a path at all). If a source PDF/text file's path is known, default to saving the note as a
   sibling file in the same directory, named after the paper's title. Don't block on this if a reasonable
   default is obvious — save it and tell the user where.
6. **When asked to process several papers in one request** (e.g. "read the agent-related ones you already
   summarized"), produce one complete note per paper rather than a combined summary — the four-question
   Method structure and two-tier Limitation don't compress across multiple papers into one file.

## Common failure modes to check for before finishing

- A Method module that only restates what it does, with no "为什么能work" reasoning distinguishable from the
  "做法" line — go back and add the actual justification, or admit in the note that the paper itself doesn't
  justify the choice (that's a legitimate, and useful, thing to note).
- A Limitation section where "我（GPT）认为的" just repeats the paper's own admitted limitations in different
  words — the second tier should surface something the paper did NOT say: an assumption it relies on without
  flagging, a failure mode outside its stated scope, or a place where its own logic (used to critique prior
  work) applies equally to itself.
- Placeholder or generic filler in any field ("待补充", "TBD", vague claims not traceable to a specific part
  of the paper) — every field should be falsifiable against the source paper.
- The two top-of-file HTML comments missing, moved elsewhere, or duplicated near the Method section.
