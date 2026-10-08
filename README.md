# WSO2 Agent Skills

Official Agent skills for building and managing with WSO2 products.

## Plugins

| Plugin | Description |
|--------|-------------|
| [api-platform](./plugins/api-platform/README.md) | Design, assess, and fix OpenAPI specs; deploy and manage APIs via the WSO2 API Gateway |
| [agent-manager](./plugins/agent-manager/README.md) | Deploy and inspect agents; tail logs, metrics, and traces; triage runtime failures |
| [integrator](./plugins/integrator/README.md) | Build integrations, automations, and services with WSO2 Integrator; installs the Ballerina plugin for the code work |
| [ballerina](https://github.com/ballerina-platform/skills) | Write, build, run, and test Ballerina code; connector discovery and `.bal` code intelligence. Installed with `integrator` |
| [healthcare](./plugins/healthcare/README.md) | Write services and integrations in Ballerina for healthcare applications, including HL7v2 and FHIR support |

## Installation

### Option 1 — npx skills

Install all WSO2 skills:
```
npx skills add wso2/agent-skills
```

This installs the `integrator` skill. The Ballerina skill it hands code work to lives in
[ballerina-platform/skills](https://github.com/ballerina-platform/skills); install it too:
```
npx skills add ballerina-platform/skills
```

### Option 2 - Claude Code

Register the marketplace:
```
/plugin marketplace add wso2/agent-skills
```

Install a plugin:
```
/plugin install api-platform@wso2-agent-skills
/plugin install agent-manager@wso2-agent-skills
/plugin install integrator@wso2-agent-skills
/plugin install healthcare@wso2-agent-skills
```

Installing `integrator` also installs `ballerina`.

**Upgrading `integrator` from 0.4.x:** `integrator` now depends on `ballerina`, and an update
does not install a new dependency on its own — until it does, `integrator` does not load. After
updating, run the install command once more:
```
/plugin install integrator@wso2-agent-skills
```

Uninstalling `integrator` leaves `ballerina` installed; remove it with `claude plugin prune`.

### Option 3 - Codex

Register the marketplace:
```bash
codex plugin marketplace add wso2/agent-skills
```

Install a plugin:
```bash
codex plugin add api-platform@wso2-agent-skills
codex plugin add agent-manager@wso2-agent-skills
codex plugin add healthcare@wso2-agent-skills
codex plugin add integrator@wso2-agent-skills
```

## Development

See [DEVELOPMENT.md](./DEVELOPMENT.md) for instructions on adding new plugins.

## License

You are free to copy, modify, and distribute these skills under the terms of the Apache 2.0 license. See the [LICENSE](./LICENSE) file for details.

