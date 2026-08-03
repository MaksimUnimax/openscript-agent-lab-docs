---
name: human-telegram-editor
description: Use when writing or revising Russian Telegram posts about AI tools, coding workflows, developer products, agents, MCP, local models, design systems, and vibe-coding. The skill turns source material into a connected, human, developer-facing Telegram post with a clear opening, one main point, plain Russian explanation, and useful practical consequence.
---

# Human Telegram Editor

## Purpose

Write a Russian Telegram post that reads like a human editor explaining one useful technical idea to developers, not like a model summarizing a video.

The post must be understandable without the source material. The reader should feel:

> “Now I understand what this is about, why it matters, and where it changes work.”

Not:

> “Someone listed facts from a video.”

This skill adapts working methods from:

- developer-facing writing: problem, system, tradeoff, practical consequence;
- content writing: hook, main argument, reader reason, flow;
- anti-AI writing: bridge sentences, no phrase stack, no empty claims;
- Russian humanizing: natural rhythm, fewer кальки, fewer English anchors, more verbs and concrete situations.

Do not create a rigid template.
Do not force an exact paragraph count.
Do not make every post use the same shape.
Do not turn the post into marketing copy.

## Core rule

A good post is not a list of facts.

A good post has:

1. a human opening;
2. one clear main point;
3. connected explanation;
4. practical consequence;
5. clean Russian voice.

If the text has correct facts but no movement of thought, rewrite it.

## Source-to-angle pass

Before drafting, do an internal source-to-angle pass and only then write the post.

1. Extract the real topic from the transcript and source facts.
2. Pick one angle that a Russian AI/dev Telegram reader will actually care about.
3. Discard unused facts that do not support that angle.
4. Shape one connected thought before naming tools or methods.
5. Treat the old `draft_text` as prior output only, not as the source of truth.

If this is a revision, do not reuse the old text as the starting point. Rebuild the angle from source facts and transcript first, then compare the new draft against the old one only after writing.

## Before writing: find the main point

Before drafting, decide the one idea the post is about. The one idea should come from the source-to-angle pass, not from the previous draft.

Ask internally:

- What problem does this solve?
- Who feels this problem?
- What changes in the work?
- What is the useful takeaway?
- What would the reader understand after this post that they did not understand before?
- Which source facts actually support this angle?
- Which facts can I ignore without losing the point?

Do not write until the main point is clear.

Bad main point:

> MCP and design systems are useful for AI agents.

Better main point:

> An AI agent writes better interface code when it sees product rules before it starts inventing components.

Bad main point:

> Local models are getting stronger.

Better main point:

> Local coding agents are useful when the project needs privacy, predictable access, or work without paid API calls.

Bad main point:

> Kilo Code supports free models.

Better main point:

> A free code agent is useful when it lets a developer test real editor workflow before choosing a paid stack.

## Opening: do not start with a definition

The first paragraph must orient the reader.

Do not start with:

- “Дизайн-система сегодня — это...”
- “Локальные модели стали...”
- “MCP решает...”
- “Context engineering отвечает...”
- “Kilo Code даёт...”
- “Главная проблема в том, что...”

Those are definition/product-note openings.

Start with a situation, tension, or recognizable problem.

Examples of better openings:

> Когда агент собирает интерфейс вслепую, он почти всегда начинает фантазировать: берёт похожий компонент, чуть меняет отступы, добавляет “удобный” блок. На макете это выглядит терпимо. В продукте — разваливает стиль.

> Бесплатный AI-инструмент обычно звучит как демо на вечер: попробовал, упёрся в лимит, пошёл дальше. Интерес начинается там, где бесплатный вариант можно поставить в редактор и проверить на настоящей задаче.

> Локальный AI для кода нужен не потому, что “облако плохое”. Он нужен в моменты, когда проект нельзя или не хочется гонять через чужой сервис: черновики, приватные файлы, нестабильный интернет, лимиты, ключи.

The opening must answer:

- where we are;
- what the problem is;
- why this is worth reading.

## Explain before naming terms

English names are allowed only when they are real names of tools or methods.

Product names may stay:

- VS Code
- Kilo Code
- LM Studio
- OpenRouter
- MCP
- OpenAI
- Claude Code

Generic English anchors should not lead the paragraph:

- agent mode
- autocomplete
- selector
- workflow
- local coding
- tool use
- context engineering
- agentic coding

Explain in Russian first. Name the term only after the reader understands the idea.

Bad:

> Context engineering отвечает за то, что модели нужно знать до старта.

Better:

> Агенту мало получить задачу. Ему нужны правила продукта до начала работы: какие компоненты брать, какие отступы разрешены, какие паттерны нельзя ломать. В англоязычной среде это часто называют context engineering.

Bad:

> В agent mode модель запускает команды и правит файлы.

Better:

> В таком режиме модель не просто подсказывает код, а работает внутри проекта: меняет файлы, запускает команды, смотрит на результат. Название может быть английским, но смысл простой — это уже не чат, а рабочий помощник в редакторе.

## Build connected explanation

Each paragraph must make the previous paragraph clearer.

Use this internal check:

> If I swap paragraph 2 and paragraph 3, does the text still read almost the same?

If yes, the text is a stack of notes. Rewrite.

A connected post usually moves like this, but do not label it and do not force the exact shape:

- situation or pain;
- why the usual approach breaks;
- what the tool/method changes;
- what this means in real work;
- limitation or practical conclusion.

This is not a template. It is a logic check.

Bad flow:

> AI needs rules.  
> MCP gives context.  
> Teams save time.  
> Product gets better.

Better flow:

> An agent breaks the interface because it does not know product rules.  
> Giving it those rules before the task changes what it can safely generate.  
> Now it can check components, colors and spacing against the same system as the team.  
> The practical win is not “more AI”, but fewer manual corrections after the first draft.

## Use concrete work situations

Prefer scenes from actual work.

Good sources of concrete explanation:

- developer opens editor;
- agent edits files;
- team reviews interface;
- component appears in the wrong style;
- model runs out of memory;
- API key or token limit gets in the way;
- prototype needs to be checked quickly;
- product team spends time on repeated corrections;
- developer compares two models on the same task.

Do not invent facts. Use only what is in source material.

But do turn facts into situations.

Fact:

> The tool supports several free open-source models.

Human explanation:

> You can try the same coding task on several free models before deciding whether the paid stack is worth it.

Fact:

> Design systems can be provided through MCP.

Human explanation:

> Instead of hoping the agent guesses the right button, you give it the same product rules the team already uses.

Fact:

> Local models depend on VRAM.

Human explanation:

> The bottleneck is not the idea of local AI. The bottleneck is the machine under your desk: how much memory it has and how much slowdown you can tolerate.

## Use Russian first

The post is for a Russian Telegram channel.

Do not write mixed phrases unless the tool name requires it.

Avoid:

- локальный agentic coding;
- agent mode;
- auto-complete модель;
- workflow;
- selector;
- tool use;
- output;
- production-ready;
- context engineering as the first explanation;
- “магия”;
- “практика упирается”;
- “на таком фоне”;
- “перестаёт звучать как компромисс”;
- “решает ключевую проблему”;
- “открывает возможности”;
- “важно не ради слова...”;

Prefer:

- локальная работа с кодом;
- режим, где модель меняет файлы и запускает команды;
- автодополнение;
- рабочий процесс;
- выбор модели;
- работа с инструментами;
- результат;
- готово для реального проекта;
- правила и контекст для агента.

Tool names stay as names. Explanations stay Russian.

## Emoji policy

This is Telegram. Emojis are useful.

Use 3–6 semantic emojis in a media post around 850–1000 characters.

Do not use only one emoji unless the post is intentionally very restrained.
Do not force every paragraph to start with emoji.
Do not decorate every claim.

Use emojis as signposts:

- 🧩 system / structure / design-system
- 🛠 work / tools / coding
- 🔍 inspection / checking / analysis
- ⚡ speed / quick start
- 🧠 model / reasoning / AI
- 🚧 limitation / caveat
- ✅ practical conclusion
- 💡 insight
- 🔒 local/private/control
- 🧪 testing / experiment

Emoji should help the reader follow the thought.

Bad:

> 🧩 title  
> paragraph  
> paragraph  
> paragraph

Better:

> 🧩 opening with the topic  
> explanation  
> 🔍 what changes  
> limitation  
> ✅ practical consequence

## Voice

Write like a smart Russian editor who understands developer work.

Not corporate.
Not academic.
Not “AI assistant explaining”.
Not over-friendly.
Not hype.

Good voice:

- clear;
- a little opinionated;
- practical;
- human;
- specific;
- calm;
- not afraid to say “this is useful only if...”.

Use verbs. AI text hides behind nouns.

Bad:

> Реализация данного подхода позволяет повысить эффективность разработки интерфейсов.

Better:

> Команда меньше правит руками, потому что агент сразу видит, какие компоненты и отступы разрешены.

Bad:

> Это снижает риски несогласованности.

Better:

> Экран меньше расползается: кнопки, цвета и сетка остаются из одной системы.

## Anti-stack checks

Reject and rewrite internally if the draft has any of these shapes:

### Definition stack

> X is...  
> Y does...  
> Z helps...  
> For teams this means...

Rewrite into one connected explanation.

### Tool-first start

> MCP does...  
> Kilo Code gives...  
> LM Studio lets...

Start with reader problem or work situation, then name the tool.

### Definition-first opening

> This tool is...  
> This method means...

Start with the situation or consequence first, not the label.

### English-term-first opening

> Agent mode...  
> Context engineering...  
> Auto-complete...

Explain in Russian first. Do not lead with the English term.

### English-anchor paragraph

> Agent mode...  
> Context engineering...  
> Auto-complete...

Explain in Russian first.

### Phrase pile

A paragraph is a phrase pile if it contains claims but no scene, consequence, or transition.

Examples:

- “это важно для разработчиков”;
- “помогает ускорить процесс”;
- “делает работу эффективнее”;
- “даёт больше контроля”;
- “снижает риски”.

These are allowed only if followed by concrete explanation.

### Swappable paragraphs

If two paragraphs can be swapped and the post still reads the same, the angle is too weak.
Rewrite until each paragraph clearly depends on the previous one.

### No bridge

If two neighboring paragraphs do not connect, add a bridge or merge them.

The reader should not ask:

> “Почему мы перескочили сюда?”

## Drafting process

Use this process internally.

### Pass 1: Point

Write the main point in one sentence after the source-to-angle pass.

If the main point is just a tool name, rewrite it.

### Pass 2: Opening

Write a first paragraph that creates situation or tension.

No definitions.
No product-note opening.
No English method name as the first anchor.

### Pass 3: Explanation

Explain the topic in plain Russian.

Name tools only after the reader understands what role they play.

### Pass 4: Work consequence

Show what changes in practice:

- less manual correction;
- faster first attempt;
- better privacy;
- less dependency on paid API;
- fewer style mismatches;
- easier model comparison;
- safer work with project files.

Pick only what is true for the source.

### Pass 5: Humanizer

Clean the Russian:

- remove кальки;
- replace generic English;
- add verbs;
- vary sentence length;
- cut corporate words;
- remove “магия” and vague praise;
- make the rhythm less even.

Do not let the humanizer turn the text back into a phrase stack or a template.

### Pass 6: Telegram read

Read it as a Telegram post.

Ask:

- would a person understand the point without the source?
- does the opening make them want to continue?
- do paragraphs connect?
- are emojis enough to guide the text?
- does any English term appear before its Russian explanation?
- does it sound like a human editor, not a model?

Rewrite if needed.

## Output requirements

- Russian language.
- Telegram-native.
- One post, one message.
- Works without the source video.
- No hashtags unless requested.
- No generic CTA.
- No source-video framing.
- No rigid paragraph count.
- No repeated template.
- Keep media-caption budget.
- Use 3–6 semantic emojis where appropriate.
- Do not split into two messages.

## Final self-check

Before final output, answer internally:

1. What is the main point?
2. What is the reader problem or work situation?
3. Does the opening create context before details?
4. Does each paragraph follow from the previous one?
5. Which English terms remain and why?
6. Are they explained in Russian?
7. Are there 3–6 useful emojis?
8. Did I remove AI-slop phrases?
9. Does the post explain the topic, not list facts?
10. Would this be understandable to a developer who has not seen the source?

If any answer is weak, rewrite.

## Scope

These are writing instructions, not lifecycle validation.
Do not add blocking state gates, approval checks, or publication blockers here.
