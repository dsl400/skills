# skills

Each skill lives in its own GitHub repository under `dsl400` and joins this
repository as a submodule that follows `main`. `write-md` is the exemplar: copy
its layout, its `README.md`, and its `.github/workflows/release.yml`.

```
<name>/                          the repository of the skill, a submodule here
  skills/<name>/SKILL.md         the skill
  skills/<name>/<files>          the tools the skill runs, next to it
  rules/<name>.md                optional: loads by `paths` and runs the skill
  README.md                      what the skill does and the reason of each check
  .github/workflows/release.yml  on a v* tag: writes the version, lints, publishes
```

The frontmatter of `SKILL.md`:

```yaml
---
name: <name>                     # kebab-case, the name of the folder
description: Use when <trigger>. # the agent picks the skill by this line; 256 characters or less
metadata:
  source: https://github.com/dsl400/<name>
  version: 0.1.0                 # the release workflow writes the tag here
---
```

```lnl
START:                                              ; entrypoint: each user message
  ASK   does the request create or change a skill?
  JUMP  REPLY IF no
  ASK   does a skill of this repository cover the need?
  JUMP  CHANGE IF yes
  ASK   does the GitHub repository dsl400/<name> exist?
  STOP  ask the human to create git@github.com:dsl400/<name>.git IF no
  DO    clone it into ./<name> and copy the layout of ./write-md
  JUMP  WRITE
CHANGE:
  DO    open ./<name>/skills/<name>/SKILL.md on the main branch of the submodule
WRITE:
  DO    write the skill: the checks, a filler and a direct sample for each check, and one lnl flow
  DO    write the reason of each check in ./<name>/README.md
LINT:
  ADD   1 to <l>
  STOP  show the diagnostics and ask the human how to continue IF <l> >= 4
  DO    run node ./lnl/skills/lnl/lnl.mjs lint ./<name>/skills/<name>/SKILL.md
  ASK   does lint print a diagnostic?
  JUMP  REPAIR IF yes
  JUMP  PUBLISH
REPAIR:
  DO    fix the line the diagnostic names
  JUMP  LINT
PUBLISH:
  DO    commit and push ./<name> to its main branch
  ASK   is ./<name> a new submodule?
  JUMP  POINTER IF no
  DO    run git submodule add <url> <name> and git config -f .gitmodules submodule.<name>.branch main
  DO    add the skill to the table of ./README.md
POINTER:
  DO    commit and push the submodule pointer of this repository
  JUMP  REVIEW

REVIEW:
  CHECK the skill lives in ./<name>/skills/<name>/SKILL.md and its tools sit next to it
  CHECK the skill names no path outside its own folder
  CHECK the description starts with "Use when" and holds 256 characters or less
  CHECK metadata.source names the repository and metadata.version holds the version of the last release or 0.1.0
  CHECK the reasons of the checks live in README.md and the skill holds the instructions
  CHECK lnl lint accepts SKILL.md and each rule of ./<name>/rules/
  CHECK each Markdown file of the turn passes the checks of ./write-md/skills/write-md/SKILL.md
  CHECK each fact lives in one skill; a second skill names the first and copies none of its text
  CHECK the submodule follows main in .gitmodules and its pointer is pushed
REPLY:
  SAY   the skill, its commit, the pointer commit, and the open diagnostics
  END
```
