# Git Repository README

Use this format for a repository's primary `README.md` or a README scoped to a
subdirectory.

## Reader task

Help a new reader quickly understand what the repository does, what it produces,
how to set it up, how to run it, and where to find deeper design information.
Match the depth to the README's scope; a component README may need only its local
contract and examples.

## Content decisions

- Lead with the repository's concrete purpose and outputs.
- Include prerequisites that readers actually need before installation.
- Present installation, execution, testing, and common query commands in the
  order readers will use them.
- Explain side effects such as downloads, generated files, overwritten outputs,
  required services, or credentials where they affect successful operation.
- Document output artifacts, important business assumptions, and operational
  constraints when they are part of the repository contract.
- Link to architecture or reference documents for detail that would interrupt
  the setup path.
- Keep examples executable and consistent with the current CLI and public API.

Avoid aspirational capabilities, generic technology descriptions, exhaustive
module tours, and repeated explanations already covered by linked documents.

## Preserve

Keep Markdown anchors, relative links, code fences, command flags, environment
variables, filenames, table schemas, and identifiers exact. Preserve badges and
generated sections when the repository uses automation to maintain them.

## Final check

- Trace every command, dependency, path, output, and behavior claim to code,
  configuration, tests, or another authoritative project source.
- Verify commands when safe and proportional to the change; otherwise state
  what was not run.
- Confirm that headings form a useful navigation path and nearby prose does not
  repeat lists or tables.
- Check Markdown syntax and links that can be validated locally.
- Read once for natural flow and once for technical drift.
