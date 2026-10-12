# skills

The skills of dsl400, one git submodule for each skill repository. Each
submodule follows the `main` branch of its repository (`branch = main` in
`.gitmodules`).

| Submodule | Skill folder |
|---|---|
| [lnl](https://github.com/dsl400/lnl) | `lnl/skills/lnl` |
| [spec-writer](https://github.com/dsl400/spec-writer) | `spec-writer/skills/spec-writer` |

## Clone

```sh
git clone --recurse-submodules git@github.com:dsl400/skills.git
git -C skills submodule foreach git checkout main
```

## Bring the submodules to the head of main

```sh
git submodule update --remote --merge
git add lnl spec-writer && git commit -m "Update the submodules"
```
