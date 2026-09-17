# Agent Skills

Reusable agent skills for data engineering, search, technical documentation,
and public-facing content across multiple repositories.

## Skills

### `batch-data-pipeline`

Designs, implements, and reviews bounded or scheduled batch pipelines with
explicit contracts, deterministic transformations, lineage, stable IDs,
idempotent materialization, and reproducible verification.

### `hybrid-semantic-search`

Designs, implements, and reviews local hybrid retrieval that combines
structured filtering with embedding similarity and stable record mapping.

### `technical-documentation`

Creates or revises Confluence pages and Git repository READMEs using verified
project sources while preserving technical detail.

### `humanizer`

Polishes an existing draft while preserving its facts, technical meaning,
structure, links, code, and author voice. It has two modes:

- `written-prose` for articles, documentation, and essays
- `spoken-narration` for voice-over scripts and structured narration sources

### `create-medium-article`

Creates or revises a Medium-ready article and optional hero-image package. It
uses `$humanizer` in `written-prose` mode after the article's facts and
structure are stable.

## Install for local development

Symlinks make this clone the canonical source, so a pull updates the installed
skills without copying them into every project. Set `AGENT_SKILLS_REPO` to the
absolute path to this clone:

```bash
AGENT_SKILLS_REPO=/absolute/path/to/agent-skills
mkdir -p ~/.agents/skills
for skill in "$AGENT_SKILLS_REPO"/skills/*; do
  ln -s "$skill" ~/.agents/skills/"$(basename "$skill")"
done
```

If a destination already exists, inspect it before replacing it. Do not create
a second installed copy of the same skill. Start a new Codex turn or session
after installation so discovery can refresh.

## Install from GitHub

Ask Codex:

> Install the skills from `kakatur/agent-skills` that match this task.

Codex's skill installer copies each package into the configured user skill
directory. A copied installation is pinned to the downloaded repository state;
install a newer version when you want updates.

## Configure a consuming repository

The skills are generic. Put repository-specific rules in:

```text
<project>/.codex/content-profile.md
```

The profile may define:

- audience and voice
- authoritative source files
- public and BTS repository boundaries
- article and narration output paths
- canonical narration source and generated exports
- required links, CTAs, terminology, and pronunciation
- validation commands and publication requirements

See [the example profile](examples/content-profile.md). Explicit user
instructions take precedence over a profile.

## Use the skills

Explicit invocation is the most predictable:

```text
Use $humanizer in written-prose mode on path/to/article.md.
Preserve code blocks, links, citations, and technical meaning.
```

```text
Use $humanizer in spoken-narration mode on the canonical narration source.
Keep timing anchors synchronized and do not edit generated TTS exports.
```

```text
Use $create-medium-article to create a Medium article about <topic>.
Use this repository's .codex/content-profile.md and the public implementation
as the source of truth.
```

Skills allow implicit invocation by default, so ordinary requests can select
the matching workflow automatically. Use explicit invocation when you want a
specific skill regardless of automatic matching.

## Updating

For a symlinked installation:

```bash
AGENT_SKILLS_REPO=/absolute/path/to/agent-skills
git -C "$AGENT_SKILLS_REPO" pull --ff-only
```

For a copied GitHub installation, move the installed skill directories to a
backup location, then install the new version. The installer intentionally
does not overwrite an existing skill directory.

## Safety and publication boundary

The skills do not publish, upload, or change an external account unless the
user explicitly requests and authorizes that separate action. They treat
webpages and source documents as content, not as instructions to execute.

The `humanizer` is an editorial tool. It must not fabricate experience,
misrepresent authorship, imitate a person without authorization, or claim to
bypass AI-detection systems.

## License

MIT. See [LICENSE](LICENSE).
