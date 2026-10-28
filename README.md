# update-recipkg-in-project

Install or update shared Recipkg project skills from their individual canonical GitHub repositories as pinned Git submodules, preserving local work and verifying consumer pointers.

Read [SKILL.md](SKILL.md) for the workflow and linked resources. This is the canonical standalone skill repository used by [Recipkg](https://github.com/recipkg/recipkg).

Where available, `recipkg skills project` can add, list and update pinned skills under `.agents/skills/`; review its staged gitlinks before committing.

## Use as a project submodule

```sh
git submodule add https://github.com/recipkg/update-recipkg-in-project.git .agents/skills/update-recipkg-in-project
git submodule update --init --recursive
```

Keep the same repository across projects. Review upstream changes and local work before checking out a new commit, then explicitly commit the consumer gitlink. Do not copy and hand-maintain a second skill or overwrite custom modifications.

This repository is also a Markdown-only Recipkg skill recipe: validate with `recipkg check .`, then pack it outside this directory. [License](LICENSE.md).

## 中文

本仓库只维护 `update-recipkg-in-project` 技能。不同项目应把此同一仓库作为固定提交的 Git 子模块引用，不复制技能正文。修改先回本仓库，再更新项目指针；注意保护本地改动。技能入口与说明见 [SKILL.md](SKILL.md)。

CLI 支持时，可用 `recipkg skills project` 添加、列出和更新 `.agents/skills/` 中的固定技能；提交前审查暂存的 gitlink。
