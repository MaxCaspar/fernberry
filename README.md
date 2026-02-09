# Fernberry Codex Skills

Fernberry is my curated set of Codex skills translated and adapted from the Taches resources for use with Codex and VS Code.

## Origin and Credit
These skills are forked and adapted from the `taches-cc-resources` repository by **glittercowboy**.

Source: https://github.com/glittercowboy/taches-cc-resources

## Inspiration and Method
I built Fernberry by leaning hard on two ideas from Taches: meta‑prompting and “skills building skills.” Using those ideas, I rebuilt and recoded his original Claude‑style skills into Codex‑native ones. Then I ran multiple conversion passes (for example, a skill whose job was to convert Claude‑native skills into Codex‑native skills), so the system could refine itself over time.

If you’re curious about the mechanics, start with the `create-skill-skill` module, which includes a Claude‑to‑Codex conversion workflow: `create-skill-skill/workflows/convert-to-codex-skill.md`.

This adaptation is deliberately formatted for Codex. I converted the original Claude‑style formatting, instructions, and logic into Codex‑native patterns so it works cleanly in Codex workflows. Please feel free to fork this repo, or even start by running the `create-skill-skill` module and build from there.

Videos that inspired this approach:
- Skills-ception: https://www.youtube.com/watch?v=LJI7FafIDg4
- Metaprompting: https://www.youtube.com/watch?v=8_7Sq6Vu0S4

## What is included
- Skill folders under `./` containing `SKILL.md` instructions and related assets.
- System skills under `./.system` used internally by Codex.

## Usage
- Clone this repo to your Codex skills path (for example `~/.codex/skills`).
- Keep it updated with `git pull`.

## License
This project is licensed under the MIT License. It includes the original MIT notice from the upstream author and additional attribution for downstream adaptations. See `LICENSE`.
