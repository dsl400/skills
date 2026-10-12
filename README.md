# skills

The skills of dsl400, one git submodule for each skill repository. Each
submodule points at a release tag.

| Submodule | Skill folder | Release |
|---|---|---|
| [lnl](https://github.com/dsl400/lnl) | `lnl/skills/lnl` | v0.3.0 |
| [spec-writer](https://github.com/dsl400/spec-writer) | `spec-writer/skills/spec-writer` | v0.1.0 |

## Clone

```sh
git clone --recurse-submodules git@github.com:dsl400/skills.git
```

## Move a submodule to a new release

```sh
git -C <submodule> fetch --tags && git -C <submodule> checkout <tag>
git add <submodule> && git commit -m "<submodule> <tag>"
```
