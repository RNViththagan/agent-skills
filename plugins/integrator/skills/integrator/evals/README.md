# integrator — promptfoo evals

Evaluates the `integrator` skill as a real agent skill discovered from the fixture
workspace. See [EVALS.md](../../../../../EVALS.md) at the repo root for the full guide.

## Run

```bash
npm install                      # installs the agent SDK(s)
# log in once (no API key needed locally):
#   claude        (Claude)   /   codex        (Codex)
npx promptfoo@latest eval -c promptfooconfig.yaml -o output.json --no-cache --no-share
npx promptfoo@latest view
```

Requires Node >= 22.22.

## Fixtures

`fixtures/workspace/` holds **real copies** of the skill under
`.claude/skills/integrator`. After editing the skill, refresh them
from the repo root with the central tool:

```bash
node tools/sync-fixtures.js integrator integrator
```

## What to fill in

`tests/triggering.yaml` and `tests/task-quality.yaml` ship with TODOs — replace
them with real cases for this skill (a positive trigger, a boundary/negative
case, and a representative task with deterministic checks + one rubric).
