# spec-rigor

Claude Code skills for writing and reviewing product specs.

| Skill | What it does |
|---|---|
| [`spec-hardening`](skills/spec-hardening/SKILL.md) | Writes or hardens a product spec until an adversarial reviewer finds nothing: ground, grid, draft, red-team, grill, apply, repeat, gate. Nothing is pushed before the gate. |
| [`spec-review`](skills/spec-review/SKILL.md) | Reviews a design pull request against the spec it builds: splits the spec into atoms, traces them to the page, runs five lenses (Letter, Reason, Figures, Ripple, Claims), reproduces each finding, and posts one GitHub review only after the gate. |

## Install

```sh
git clone git@github.com:tonymorony/spec-rigor.git ~/devel/spec-rigor
ln -s ~/devel/spec-rigor/skills/spec-hardening ~/.claude/skills/spec-hardening
ln -s ~/devel/spec-rigor/skills/spec-review ~/.claude/skills/spec-review
```

## Sources

- The structure follows Matt Pocock's [`writing-for-agents`](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-for-agents) (steps with completion criteria, disclosed reference, leading words).
- `spec-review/atoms.py` reads specs with BR, EC and OQ tables, and prose specs.
- `spec-hardening/spec_lint.py` checks a spec for duplicate and dangling IDs, line-number code citations, missing paths and, in a stack, IDs that a higher slice already uses.
