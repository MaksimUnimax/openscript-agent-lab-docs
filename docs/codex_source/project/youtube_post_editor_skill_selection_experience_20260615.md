# YouTube Post Editor Skill Selection Experience — 2026-06-15

Status: imported from ChatGPT dialogue
Scope: `youtube_post_editor_agent`, Telegram post draft wording, source-to-angle editing, editor skill selection
Do not treat this as a product fix. This is a lessons-learned document for future editor-agent work.

## Why this document exists

During the YouTube post publisher/editor work, the project repeatedly tried to improve the output of the internal `youtube_post_editor_agent`.

The visible problem was not just “bad style”. The agent kept producing Telegram post drafts that sounded like:
- dry summaries;
- disconnected fact stacks;
- definition stacks;
- product notes;
- English/Russian hybrid text;
- pseudo-human AI prose;
- posts without a real human opening or clear topic.

This document records what was tried, what helped, what failed, and what must not be repeated.

## Current accepted lesson

The editor agent must not only “write humanly”.
It must first transform source material into an editorial angle:

source transcript / source facts
→ one useful topic
→ reader problem or tension
→ practical consequence
→ connected Telegram post

Without that source-to-angle step, the model keeps turning source material into a stack of correct but weak facts.

## Important proof: regeneration source

A proof run showed that `regenerate_text_requested` does not rewrite the previous draft as its main input.

The text regeneration path uses the same editor-contract request shape as initial generation:
- `source_facts_snapshot`
- `transcript_snapshot`
- `editorial_constraints`
- `editorial_rules`
- `grounding`

The request does not include old `draft_text`.
Previous draft text is used only after the model returns for no-op comparison/update logic.

Transcript snapshots were present for the inspected drafts:
- `post-draft-aa6589f0fe2c`: transcript length about 3985 characters
- `post-draft-bc7a951fa811`: transcript length about 3472 characters
- `post-draft-a2dc0520ab53`: transcript length about 49014 characters

Conclusion:
Repeated weak wording was not caused by old-draft reuse or missing transcript/source context.
The weakness was in editorial transformation.

## Skills and sources tried

### 1. `talkstream/ru-text`

Purpose tried:
- Russian text quality
- info-style
- anti-cancellaria
- clarity
- anti-pattern cleanup

What helped:
- reminded that text must serve the reader;
- pushed toward concrete meaning instead of vague claims;
- useful for cleaning Russian wording.

What did not solve the problem:
- it did not build a Telegram post angle;
- it did not by itself create a human opening or narrative movement;
- output could still be clean but dry.

Lesson:
Use ru-text principles as a cleanup layer, not as the main writing strategy.

### 2. `coreyhaines31/marketingskills` — social, copywriting, copy-editing

Purpose tried:
- social post thinking;
- standalone content atom;
- benefit over feature;
- specificity;
- editing passes.

What helped:
- “standalone post” and “so what?” were useful ideas;
- helped move away from video recap;
- helped define why a post must work without the source video.

What failed:
- used too broadly, it became another list of abstract writing rules;
- it did not guarantee a human explanatory flow;
- copywriting/copy-editing language risked moving the post toward marketing/product-note tone.

Lesson:
Useful as supporting principles, but not enough as the main skill.

### 3. `ilyautov/humanizer-ru`

Purpose tried:
- remove Russian AI-slop;
- reduce кальки and English-biased Russian;
- improve rhythm;
- remove phrases like “магия”, “практика упирается”, awkward generic wording.

What helped:
- improved some surface language;
- reduced obvious AI-ish phrases;
- helped catch bad wording and English/Russian hybrid phrases.

What failed:
- it did not build the topic;
- it cleaned bad text but did not create a good post;
- output still became “cleaned note”, not human explanation.

Lesson:
Humanizer belongs as a final cleanup pass, not as the main editorial framework.

### 4. `Stahlwalker/developer-marketing`

Purpose tried:
- developer-facing writing;
- respect developer time;
- show practical system/tradeoff;
- avoid vague marketing.

What helped:
- moved the post toward practical developer consequences;
- helped with “what changes in actual work”.

What failed:
- when used as the main frame, it pulled output into technical/product-note phrasing;
- produced artificial patterns like “not X, but Y” and “if X, then Y”;
- examples became templates the model imitated.

Lesson:
Use only small principles:
- specificity;
- respect developer time;
- show how it works.
Do not use it as the whole post structure.

### 5. `ComposioHQ/content-research-writer`

Purpose tried:
- hook;
- main argument;
- audience;
- flow;
- transitions;
- voice preservation.

What helped:
- revealed the missing step: before writing, decide the main argument/angle;
- helps avoid immediate fact dumping;
- useful for connected explanation.

What failed or risked:
- as a full article workflow it is too broad for a Telegram caption;
- if overused, it may create blog-like structure.

Lesson:
Use the core idea: find the angle before writing.
Do not import a long article workflow.

### 6. `conorbronsdon/avoid-ai-writing`

Purpose tried:
- avoid AI-ish text patterns;
- add bridge sentences;
- detect paragraph stacks;
- remove empty intensifiers and generic AI vocabulary.

What helped:
- “missing bridge sentences” is a key diagnostic;
- if paragraphs can be swapped without breaking logic, the text is a stack of notes;
- useful for detecting fake connectedness.

What failed or risked:
- not a complete source-to-post editor skill;
- mostly a cleanup / anti-pattern layer.

Lesson:
Use the anti-swap / bridge check, not the whole skill as a post generator.

## Important technical fixes discovered during skill work

### Prompt assembly and truncation mattered

A proof run showed:
- `human_telegram_editor.md` existed and synced to runtime;
- but the live assembled prompt included only an early fragment of it;
- the strongest anti-fact-stack and self-check sections were truncated;
- `telegram_style_guard.md` was not loaded into the prompt at all;
- service scaffold still pushed `5-7 short paragraphs`, emoji-led paragraphs, and roundup/news framing before the skill.

Fix made:
- `telegram_style_guard.md` was prioritized into editor training context;
- `human_telegram_editor.md` self-check survived in assembled prompt;
- old single-topic scaffold pressure was removed/narrowed;
- prompt no longer forced every paragraph to start with emoji;
- digest/news examples no longer dominated single-topic drafts.

Lesson:
If a skill exists on disk but is truncated or lower-priority than scaffold instructions, it is effectively not applied.

### Blocking quality gate was a mistake

A deterministic quality gate was briefly made blocking.
That blocked draft moderation delivery for editorial quality issues.

User rejected this approach.

Fix made:
- editorial quality findings were converted to advisory diagnostics;
- hard validation remains only for true contract/safety issues;
- editorial warnings must not block Telegram/operator moderation delivery.

Lesson:
Do not add lifecycle blockers for taste/editorial quality.
The operator must be able to review bad drafts in Telegram.
Quality diagnostics are advisory, not a publication/moderation delivery gate.

### Title overlay was a separate issue

The illustration title overlay work was a rendering/layout problem, not a text skill problem.

Resolved direction:
- title remains on the illustration;
- agent may generate the title wording;
- image generator should generate clean base illustration;
- Python script overlays the title onto image;
- title overlay layout was improved into an editorial lower-third plate.

Lesson:
Do not mix overlay/image work with editor text skill work.

## What caused regressions

### Too many examples became templates

The skill included many bad/better examples.
The model copied their rhythm instead of applying the principle.

Bad recurring patterns appeared:
- “не X, а Y”
- “если раньше..., то теперь...”
- “главный смысл не в...”
- “главная проблема...”
- “это уже не игрушка...”
- “важнее громких обещаний...”

Lesson:
Examples must be used sparingly.
Avoid examples that can become reusable phrases.

### Too much checklist language created checklist prose

Instructions like:
- main point;
- opening;
- work consequence;
- bridge sentences;
- emoji count;
- pass 1 / pass 2 / pass 3

were correct as editor analysis but made the model write as if answering a checklist.

Lesson:
Keep editor thinking internal, but do not let it become a visible fixed structure.

### Humanizer alone is not enough

Humanizer improved surface language but did not solve:
- what is the post about;
- why should the reader care;
- what is the connected explanation.

Lesson:
Humanizer belongs after source-to-angle, not before it.

### Developer-marketing as main style was too product-note-like

It made posts more practical but also more synthetic and product-ish.

Lesson:
Use developer-marketing only for specificity and practical consequence.

## What worked best

The strongest improvement came from the final source-to-angle update.

The skill now has to do this internally:
1. extract the real topic from transcript/source;
2. pick one angle;
3. discard facts that do not support that angle;
4. start from reader situation/problem, not tool label;
5. explain in Russian before naming tools;
6. shape the post as one connected thought;
7. avoid swappable paragraphs and phrase stacks;
8. keep semantic emoji, but not as a mechanical target;
9. avoid lazy generated turns.

This is the current preferred direction.

## Current stop-point

The latest text regeneration after source-to-angle update delivered refreshed Telegram moderation cards:

- `post-draft-aa6589f0fe2c` -> message id `1148`
- `post-draft-bc7a951fa811` -> message id `1150`
- `post-draft-a2dc0520ab53` -> message id `1152`

The output is more acceptable than earlier versions but still not a final solved editorial system.
The user judged the current result acceptable enough to proceed, but wants this learning saved before restarting the pipeline.

No publication approval was performed as part of this editor work.

## Current source/runtime state caveat

During this work, multiple source files were modified in the working tree and not necessarily committed/pushed at each intermediate step. Reports named changed areas including:
- `agent-packages/youtube_post_editor_agent/**`
- `agent_lab/youtube_image_title_overlay.py`
- `agent_lab/youtube_post_draft_service.py`
- `tests/test_youtube_image_title_overlay.py`
- `tests/test_youtube_post_draft_service.py`

Runtime profile copies for the editor skills were applied through `agentctl apply` during proof runs.

Before any final source commit/publication-proof block, verify current git state and decide what should be committed.

## Do not repeat

Do not repeat these failed approaches without fresh proof:

- do not add a blocking editorial quality gate;
- do not keep regenerating with the same skill if source-to-angle is missing;
- do not assume text regeneration uses the previous draft;
- do not search random skills and paste them wholesale;
- do not let Codex choose writing skills;
- do not use many bad/better examples that become templates;
- do not mix image overlay layout work with text skill work;
- do not mark Codex subjective quality status as proof;
- do not trust “human_editorial_status=pass” unless visible output supports it.

## Recommended future editor-improvement direction

Future work should focus on:
- better source-to-angle extraction;
- better invisible angle planning;
- fewer visible examples;
- more natural Russian editorial rhythm;
- short comparative review of output before sending;
- using advisory diagnostics, not blockers;
- creating a small corpus of accepted/rejected Telegram posts for taste calibration.

A future separate research task may look for stronger Russian narrative/editorial skills, but only after recording what has already failed.
