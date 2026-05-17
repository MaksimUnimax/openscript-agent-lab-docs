TITLE: Technical Spec Extension v0.4 — Fin Instrument Tab, Agent Farm, and Agent Tools
STATUS: IMPORTED_PRODUCT_DIRECTION_UPDATE
SOURCE_KIND: chatgpt_inline_user_clarification
DATE: 2026-05-17
RELATION_TO_TZ_V0_3: extends v0.3, does not replace it
CURRENT_PRIORITY: finish Fin Instrument / Financial Tool first, keep Agent Farm deferred, then revisit shared runtime architecture later

## 1. Why this update exists

The user clarified the next product direction and corrected the UI/module placement.

The financial tool must not be designed as a separate new UI tab.

The current UI tab named “Телеграмм” is already specialized around:
- the financial agent workflow;
- Telegram bot input;
- voice for the financial agent;
- the next planned Telegram user_id allowlist/access-control step.

The correct product direction is:
- rename the current “Телеграмм” tab to “Фин инструмент”;
- continue the immediate Telegram user_id allowlist work inside that same “Фин инструмент” tab;
- continue financial tool development in that tab;
- treat this as the financial tool surface that agents will use.

This is a documentation/product-direction update, not an implementation request.

## 2. Immediate current priority

Immediate priority remains:
- close access to the Telegram bot;
- implement Telegram user_id allowlist/access control after task-card re-evaluation;
- deny unknown users before any resource use;
- use Telegram `from.id` / `user_id` for allowlist identity;
- do not use `chat_id` as the allowlist identity.

Placement:
- this work belongs in the current tab now called “Телеграмм”;
- planned product label for that tab is “Фин инструмент”;
- do not create a separate new tab for this access-control / financial-tool line.

## 3. “Фин инструмент” meaning

“Фин инструмент” is not just Telegram settings.

It is the financial tool surface for agents.

It should contain and own the product line for:
- Telegram user access control for the financial bot/tool;
- voice settings for the financial-agent workflow;
- receipt handling;
- future financial database/storage controls;
- scripts for safe writes and reads;
- reports and summaries;
- tool status and readiness;
- later financial workflow controls if needed.

The name “Фин инструмент” makes the surface look like a tool used by agents, not just a Telegram integration page.

## 4. Financial Agent Business Tool clarification

Important clarification:
it is not just a database.

It is a business tool / tool package for financial agents.

It should include:
- database schema and storage;
- deterministic scripts;
- safe write and read operations;
- receipt reading and parsing;
- confirmation flow if needed;
- expense and income records if designed later;
- reports and summaries;
- audit fields;
- compact factual result returned to the agent.

The financial agent must not:
- write SQL directly;
- mutate the DB directly;
- invent totals;
- bypass scripts;
- store secrets in git;
- confirm receipt facts without user confirmation if confirmation is part of the flow.

The financial agent may:
- ask clarifying questions;
- explain factual results;
- format answers;
- apply character/style;
- call allowed financial business tools.

The tool owns:
- DB writes;
- DB reads;
- calculations;
- receipt ingestion;
- normalized records;
- reports;
- validation.

## 5. Updated product direction after access control

After access to the Telegram bot is closed, the project should expand into a universal multi-agent farm.

The farm should support:
- many agents;
- different agent roles;
- separate agent instructions;
- separate tools per agent or per task type;
- runtime/task logic for launching agent tasks;
- assignment of tasks to agents;
- tracking execution progress;
- observing whether tasks completed, failed, or need repair;
- future task-specific tools and business layers.

This expands the project beyond the initial financial-agent scenario but does not remove the financial scenario.

## 6. Correct ordering after this update

Current active near-term order:

1. Task-card re-evaluation:
   - `telegram_user_id_allowlist_ui`;
   - include placement decision: current “Телеграмм” tab should become “Фин инструмент”.

2. Access-control implementation after task-card readiness:
   - Telegram user_id allowlist;
   - placed in “Фин инструмент” tab;
   - deny-before-resource-use.

3. Rename/current tab direction:
   - current “Телеграмм” tab becomes “Фин инструмент” in product/UI vocabulary;
   - this should be implemented only in a later approved fix-run.

4. Agent Farm / Task Runtime design/proof:
   - task model;
   - task runtime;
   - agent execution targets;
   - task status and monitoring;
   - tool assignment boundaries;
   - no hardcoded agent count.

5. Financial Agent Business Tool design/proof:
   - inside “Фин инструмент” product area;
   - not raw DB exposed to agents;
   - deterministic business tool with scripts and receipt handling.

6. Future tool families:
   - Telegram Post Publisher Agent/Tool;
   - YouTube Parsing Agent/Tool;
   - other task tools TBD.

## 6.1 Priority correction: finish Fin Instrument first

The active near-term order is corrected again after the later proof/design work:

1. finish the Telegram access/auth/no-silent-reply line when needed;
2. continue the Financial Agent Business Tool inside “Фин инструмент”;
3. treat the shared Agent Farm / Task Runtime question as deferred until Fin Instrument is progressed;
4. decide later whether the runtime architecture is common for all agents, per-tool, or hybrid;
5. keep Telegram Post Publisher and YouTube Parser as later tool families.

Historical ordering in this document remains as context, but the active priority is the Fin Instrument / Financial Tool line first.

## 7. Telegram Post Publisher Agent/Tool

Planned direction:
- create an agent/tool line for publishing posts to Telegram;
- this should be a separate task/tool family, not mixed into financial agent logic;
- it should eventually support creating, reviewing, scheduling, and publishing posts;
- it must not be confused with Telegram access-control in “Фин инструмент”;
- it needs separate vendor docs and safety checks before implementation.

Status now:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF.

Do not implement now.

## 8. YouTube Parsing Agent/Tool

Planned direction:
- create an agent/tool line for YouTube parsing;
- it may eventually parse channels, videos, metadata and transcripts depending on later design;
- it must be separate from financial tool and Telegram publisher;
- it needs vendor / legal / API / docs proof before implementation.

Status now:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF.

Do not implement now.

## 9. Other future agent tasks

The user said several other future tasks are planned but not specified yet.

Record them only as:
- future task tools TBD;
- status: PLANNED_PLACEHOLDER / NEEDS_SPEC;
- no implementation;
- no module ownership until a concrete task is specified.

## 10. Module / architecture implications

New or clarified planned module families:

1. Fin Instrument UI Surface
Purpose:
- renamed/current “Телеграмм” tab;
- financial tool control surface;
- Telegram user_id allowlist placement;
- voice/Telegram settings for financial-agent workflow;
- future financial business tool status/settings.

Status:
- PLANNED / NEEDS_TASK_CARD_REEVALUATION / NEEDS_DESIGN / NEEDS_PROOF.

2. Agent Farm / Task Runtime
Purpose:
- task creation;
- task assignment;
- execution target selection;
- status tracking;
- progress monitoring;
- result artifacts;
- repair/retry policy later.

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF.

3. Financial Agent Business Tool
Purpose:
- database + scripts + receipt ingestion + reports;
- deterministic finance operations for financial agents;
- lives under the “Фин инструмент” product direction.

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF.

4. Telegram Post Publisher Tool
Purpose:
- post creation / review / schedule / publish to Telegram.

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF.

5. YouTube Parsing Tool
Purpose:
- parse YouTube sources for future agents and tasks.

Status:
- PLANNED / NEEDS_DESIGN / NEEDS_PROOF.

6. Future Tools TBD
Purpose:
- placeholder for not-yet-specified future task tools.

Status:
- PLANNED_PLACEHOLDER / NEEDS_SPEC.

## 11. Safe boundaries for the expanded direction

- Do not make a separate new tab for the financial tool if the current “Телеграмм” tab is the intended financial tool surface.
- Do not mix Telegram access-control with Telegram post publishing.
- Do not mix Telegram publisher with the financial “Фин инструмент” line.
- Do not make one god module for agent farm, finance, Telegram publishing and YouTube parsing.
- Do not put task runtime logic into random UI files.
- Do not put financial DB writes inside agent prompt/code.
- Do not let agents write SQL.
- Do not treat the financial DB as a raw database exposed to agents.
- Do not implement YouTube parsing without separate docs/proof.
- Do not implement new external integrations without vendor/legal/API source docs.
- Do not hardcode current agents.
- Do not hardcode one user/chat/provider unless a proof task explicitly allows it.
- Do not mark any new tool family DONE from this docs update.

## 12. Task card implications

After this docs update:
- `telegram_user_id_allowlist_ui` remains the immediate next task-card re-evaluation;
- that re-evaluation must account for placement:
  - current “Телеграмм” tab should be renamed / treated as “Фин инструмент”;
  - allowlist belongs there.

New future task cards may exist but must remain not ready:
- `fin_tool_tab_rename_and_allowlist_ui`
- `agent_farm_foundation`
- `financial_agent_business_tool`
- `telegram_post_publisher_agent`
- `youtube_parsing_agent`

All new task cards, if created, must be `ready_for_fix_run: false`.
They require separate design/proof before implementation.

## 13. Current active block after this update

Active block:
- Telegram user_id allowlist UI task-card re-evaluation.
- Include “Фин инструмент” tab placement/rename decision in that re-evaluation.

Next after allowlist:
- Agent Farm / Task Runtime design/proof.

Next after farm foundation:
- Financial Agent Business Tool design/proof inside the “Фин инструмент” direction.

Parallel/future after that:
- Telegram Post Publisher Agent/Tool;
- YouTube Parsing Agent/Tool;
- other task tools TBD.
