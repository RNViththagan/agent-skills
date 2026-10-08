# integrator — promptfoo evals

Evaluates the `integrator` skill as a real agent skill discovered from the fixture
workspace. See [EVALS.md](../../../../../EVALS.md) at the repo root for the full guide.

## Run

```bash
npm install                      # installs the agent SDK(s)
# log in once (no API key needed locally):
#   claude        (Claude)   /   codex        (Codex)
npx promptfoo@latest eval -c promptfooconfig.yaml -o output.json --no-cache --no-share
npx promptfoo@latest eval -c promptfooconfig.no-ballerina.yaml --no-cache --no-share
npx promptfoo@latest view
```

There are two configs. `promptfooconfig.yaml` enables the `integrator` and `ballerina` skills
and runs `tests/triggering.yaml` and `tests/task-quality.yaml`. `promptfooconfig.no-ballerina.yaml`
enables only `integrator`, so the Ballerina skill is genuinely unavailable, and runs
`tests/missing-ballerina.yaml`.

Results vary between runs; use `--repeat 3` and treat a test as passing when it passes at
least two of three.

Requires Node >= 22.22.

## Fixtures

`fixtures/workspace/` holds:

- `.claude/skills/integrator` — a **real copy** of the skill. After editing the skill, refresh it
  from the repo root with `node tools/sync-fixtures.js integrator integrator`.
- `.claude/skills/ballerina` — a hand-written stub carrying only the Ballerina skill's
  description, so triggering tests have a competitor. `sync-fixtures.js` does not touch it; keep
  its description in step with ballerina-platform/skills.
- `projects/multi` and `projects/single` — read-only sample projects (one with several
  integrations, one with a single integration) that the layout tests point at.
