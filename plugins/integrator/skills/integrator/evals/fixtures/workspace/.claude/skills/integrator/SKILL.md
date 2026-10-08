---
name: integrator
description: Entry point for WSO2 Integrator work. Use when the user is building or changing a
  WSO2 Integrator project — adding an integration, an automation, a service, or a library
  integration, wiring connectors between systems — or names WSO2 Integrator. Applies WSO2
  Integrator conventions and hands the code work to the Ballerina skill, or gives the command
  to install it when it is missing. Not for general Ballerina language questions or Ballerina
  code that has nothing to do with WSO2 Integrator; those go straight to the Ballerina skill.
---

# WSO2 Integrator

This skill sets how work is shaped in WSO2 Integrator. The Ballerina skill writes, builds, runs,
and tests the code.

## Workflow

1. **Check the Ballerina skill is available.** If it is not, stop and give the user the install
   command from [If the Ballerina skill is missing](#if-the-ballerina-skill-is-missing). You cannot
   install skills yourself, and do not write the integration's code without it.
2. **Shape the work with the conventions below** — where the code goes, what kind of integration
   it is, how configuration is declared.
3. **Hand the code work to the Ballerina skill** for writing, building, running, testing, and
   library lookup. Pass on the conventions that apply.
4. **Check your words before you reply.** Name what you built: "the new `ftp_to_salesforce`
   integration", "your project". Outside TOML section names, no "workspace" and no "package" —
   not in prose, headings, file labels, comments, or tables.

## Which skill does the work

| Request | Skill |
|---|---|
| Write, build, run, test, or debug integration code | Ballerina skill (`ballerina`) |
| Find a connector or library and its API | Ballerina skill — its `library` agent |
| Migrate a Mirth Connect channel, HL7v2, or FHIR integration | `mirth-to-ballerina` (WSO2 Healthcare plugin) |

## If the Ballerina skill is missing

- **Claude Code:** installing `integrator` installs it automatically. If it is still missing —
  usually after updating from an earlier version of this plugin — run
  `/plugin install integrator@wso2-agent-skills` again, or
  `/plugin install ballerina@wso2-agent-skills`.
- **Other agents (Codex, Cursor, Gemini CLI, Copilot, …):** `npx skills add ballerina-platform/skills`

## WSO2 Integrator conventions

- **Words.** A Ballerina workspace is a **project**; a Ballerina package is an **integration**.
  Write "the project's root `Ballerina.toml`" and "declares `shared_utils` as an integration".
  "Workspace" and "package" appear only as the TOML section names `[workspace]` and `[package]`.
- **Project layout.** The root `Ballerina.toml` holds only a `[workspace]` section with a
  `packages` array. A new integration is a directory with its own `Ballerina.toml`
  (`[package]` with `org`, `name`, `version`), added to that `packages` array. Prefer changing an
  existing integration over creating a new one unless the user asks for a new one.
- **Library integrations.** An integration meant to be reused by others must contain `lib.bal`
  with `import wso2/strict.library as _;` — without it the integration is treated as a regular
  one.
- **Automations.** An automation is an integration with a `main` function unless the user asks
  for a service. Schedules such as "every hour" or a cron expression are configured where the
  integration is deployed (Kubernetes or the integration platform), not written into the code —
  when the user asks for one, tell them that is where it goes.
- **Configurables.** Declare configurables only as `string`, `int`, `byte`, `float`, `decimal`,
  `boolean`, or arrays of them — never a subtype such as `int:Signed32`, even when a connector
  method takes one; widen to the base type and cast at the call. Never give a configurable a
  default value. The one exception is an OAuth `refreshUrl`, which may default to the provider's
  token endpoint.
