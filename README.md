# skills

The skills of dsl400, one git submodule for each skill repository. Each
submodule follows the `main` branch of its repository (`branch = main` in
`.gitmodules`).

| Submodule | Skill folder |
|---|---|
| [brand](https://github.com/dsl400/brand) | `brand/skills/brand-builder`, `brand/skills/brand-check` |
| [lnl](https://github.com/dsl400/lnl) | `lnl/skills/lnl` |
| [recall](https://github.com/dsl400/recall-skill) | `recall/skills/recall` |
| [rocket-launcher](https://github.com/dsl400/skill-rocket-launcher) | `rocket-launcher/skills/rocket-launcher` |
| [spec-writer](https://github.com/dsl400/spec-writer) | `spec-writer/skills/spec-writer` |
| [write-md](https://github.com/dsl400/write-md) | `write-md/skills/write-md` |
| [youtube](https://github.com/dsl400/skill-youtube) | `youtube/skills/youtube` |

## Clone

```sh
git clone --recurse-submodules git@github.com:dsl400/skills.git
git -C skills submodule foreach git checkout main
```

## Bring the submodules to the head of main

```sh
git submodule update --remote --merge
git add brand lnl recall rocket-launcher spec-writer write-md youtube && git commit -m "Update the submodules"
```
