# HTML Prototype to Frontend

A Codex skill for converting an existing HTML/CSS/JavaScript prototype into a frontend framework or component system while preserving its rendered UI, relevant interactions, and outputs.

The workflow starts from the prototype source, keeps its structure and visual rules, then checks the result in the real application at the same content width, font, time, and data. It is framework agnostic; React-specific guidance lives in `references/react.md` and is loaded only for React work.

## Contents

- [`SKILL.md`](SKILL.md): conversion and verification workflow
- [`references/parity.md`](references/parity.md): shared visual, data, and state checks
- [`references/react.md`](references/react.md): React state and lifecycle notes

## Install

Copy this repository into a Codex skills directory as `html-prototype-to-frontend`:

```bash
mkdir -p ~/.codex/skills
cp -R html-prototype-to-frontend ~/.codex/skills/html-prototype-to-frontend
```

Then invoke `$html-prototype-to-frontend` or let Codex select it for a matching prototype conversion task.
