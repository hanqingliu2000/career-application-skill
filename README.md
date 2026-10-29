# Career Application Skill

[中文说明](README.zh-CN.md)

A reusable agent skill for building a career evidence base, researching employers and jobs, and preparing a targeted resume. Designed for Codex and Claude Code using the shared Agent Skills `SKILL.md` format.

## What it does

- **Career evidence base:** Organizes user-provided past resumes, application materials and other evidence into a maintainable, source-aware profile while preserving originals and unresolved conflicts.
- **Experience interview:** Uses the required `grilling` skill to uncover context, individual contributions, decisions and measurable outcomes. It does not suggest personal facts.
- **Employer and job research:** Checks official sources, current availability and requirements; separates actual job fit from application status and unknowns.
- **Resume tailoring:** Builds a role-specific narrative grounded in verified evidence, explains internal terminology and preserves the boundaries of claims and metrics.
- **Three independent reviews:** Separately evaluates expression and consistency, hiring relevance, and rendered layout. The primary agent verifies facts and brings the findings to the user before implementing approved changes.
- **Application checks:** With explicit authorization, checks the live role, selected attachments and populated answers. It reports submission only when confirmation is observed.

Each stage can be requested separately. This project contains instructions, not an automatic application bot or a guarantee of interview outcomes.

## Requirements

- **Required skill:** [`grilling` by Matt Pocock](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md). Install it separately and make it available to the same agent. It is required for the experience interview; if unavailable, the interview pauses while independent work may continue. Personal-history questions must not be answered with invented recommendations.
- Codex or Claude Code with skill support. Web access is needed for live research; document rendering tools are needed for visual checks.
- **Isolated review requires an environment that enforces and verifies restricted file, network and tool access for each reviewer.** Separate chats or subagents alone do not establish isolation. This repository supplies the protocol, not an isolation runtime. If it cannot be enforced, the agent must say so and ask before using a reduced review; it must not claim the full review passed.

## Install

Clone this repository and the required upstream repository, then copy both skill directories to the appropriate skill directory. Inspect third-party code and instructions before installation. The paths below assume the repositories have been cloned as `career-application-skill` and `mattpocock-skills` in the current directory. Replace those paths if needed. Do not overwrite an existing skill without reviewing it.

```bash
git clone https://github.com/hanqingliu2000/career-application-skill.git
git clone https://github.com/mattpocock/skills.git mattpocock-skills
```

**Codex — personal skills:**

```bash
mkdir -p ~/.agents/skills
cp -R career-application-skill/skills/resume-application ~/.agents/skills/
cp -R mattpocock-skills/skills/productivity/grilling ~/.agents/skills/
```

**Claude Code — personal skills:**

```bash
mkdir -p ~/.claude/skills
cp -R career-application-skill/skills/resume-application ~/.claude/skills/
cp -R mattpocock-skills/skills/productivity/grilling ~/.claude/skills/
```

Restart the agent session if necessary and check that both skills are discoverable. Codex can invoke `$resume-application`; Claude Code can invoke `/resume-application`. The skill directs the agent to invoke `grilling` when conducting the experience interview. Paths and availability can differ in cloud or managed environments; consult the platform documentation.

## Examples

- “Use the resume application skill to organize the application materials I provide into a career evidence base.”
- “Interview me about my project contributions and update the evidence base.”
- “Research the employers on my list and identify current roles that fit my experience.”
- “Tailor my resume to this job description and run the three isolated reviews.”

The agent should ask before taking an actual submission action and should not treat a job link or a prepared resume as submission authorization. Keep personal records and generated application materials in a private workspace, not in a public repository.

## Project layout

`skills/resume-application/SKILL.md` routes to focused references for career evidence, job research and resume review. The `grilling` dependency is maintained upstream and is not bundled here.

## Platform documentation

- [Codex skills](https://developers.openai.com/codex/skills)
- [Claude Code skills](https://code.claude.com/docs/en/skills)
