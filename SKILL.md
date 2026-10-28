---
name: update-recipkg-in-project
description: Install or update shared Recipkg project skills from their individual canonical GitHub repositories as pinned Git submodules, preserving local work and verifying consumer pointers.
---

# Install or update shared Recipkg project skills

## Canonical sources

Each skill has its own repository at `https://github.com/recipkg/<skill-name>.git`. Use the reviewed catalog in the project's `migrate-to-recipkg/PROJECT_SKILLS.md`; if migration is not installed yet, inspect [its canonical repository](https://github.com/recipkg/migrate-to-recipkg) and add it first. A project should reference the same upstream skill repositories, not duplicate their files or create project-specific forks.

## Procedure

1. Inspect project instructions, Git status, `.gitmodules`, existing skill directories, submodule remotes/commits, and local edits. Use the project's agent directory, normally `.agents/skills/`.
2. For each catalog entry, reuse an existing correct submodule. If the target path is free, add its own repository with `git submodule add https://github.com/recipkg/<skill-name>.git .agents/skills/<skill-name>`. Never add the whole Recipkg checkout merely to obtain a skill.
3. An existing ordinary directory is not a submodule. Compare its content/provenance with upstream, preserve custom work, and convert only when its ownership and migration scope are established. Do not delete unknown content or overwrite edited skills.
4. Initialize recursive submodules. Verify YAML metadata and references, repository URL, reviewed commit, and parent gitlink mode `160000`.
5. For updates, record the current pin and check dirty state, fetch without resetting, inspect candidate changes, and check out a reviewed full commit. Detached HEAD is normal for a pinned submodule. Do not blindly follow a branch or run a forced recursive update.
6. Run local checks and review `.gitmodules`, submodule status, and pointer diffs. Commit only the authorized metadata/gitlinks and relevant documentation. A GitHub topic or successful clone does not prove the skill's behavioral quality.

## CLI and generated source

A globally installed `recipkg` CLI can be used separately; `skills sync` creates managed copies for non-Git destinations and does not fulfill this submodule workflow. If a Recipkg source checkout is explicitly needed, initialize it recursively and install the CLI from `generated/cli-source/`. `generated/` is a container whose child source repositories are submodules; never flatten implementation files into it.

Upstream edits belong in each skill's repository, then consumers explicitly update their pins. Keep project-specific notes outside upstream skill files. Preserve other skills, data, and source submodules. Use local verification; do not add or trigger CI unless it is requested. Existing CI that must consume submodules needs recursive checkout and least-privilege credentials, without assuming a developer's local environment.

## 中文

每个技能对应 `recipkg/<skill-name>` 独立仓库。读取迁移技能中的 `PROJECT_SKILLS.md`，让宿主项目把相同仓库作为固定提交的子模块添加到 `.agents/skills/`（或沿用现有 agent 目录），不要再整仓加入 Recipkg 后手工同步技能副本。已有普通目录先核对来源并保护自定义内容；dirty 子模块先处理本地工作，不能强制更新。更新先回技能上游，再审查并显式提交宿主 gitlink；用 `160000`、remote、提交和实际文件确认不是普通文件夹。

CLI 独立安装；如明确需要源码 checkout，从递归初始化后的 `generated/cli-source/` 安装。`generated/` 只作容器，里面每个源码子目录必须是独立 Git 仓库的固定提交子模块。
