## Changelog

此项目的所有显着更改将记录在此文件中。

格式基于 [维护日志](https://keepachangelog.com/zh-CN/1.0.0/) ，
并且该项目遵循 [语义版本控制](https://semver.org/spec/v2.0.0.html) 。

在 `GitHub` 提交消息上使用的表情符号基于 [gitmoji](https://gitmoji.carloscuesta.me/) 。

## [Unreleased]

### ✨ 增加

- 📝 增加 [cache 使用方法](./README.md#actionscache-的使用方法)
- 🔧 增加 [list](./template/sync2gitee.list.yml) 模板
- 📝 增加 [如何挑选模板](./README.md#如何挑选模板) 说明

### ♻️ 变化

- 💬 更新[关于创建仓库失败的说明内容](./README.md##gitee-无法创建-xxx-仓库如何解决)
- ⬆️ 升级 hub-mirror-action 到 [v0.10](https://github.com/marketplace/actions/hub-mirror-action)

### 🔥 移除

- 🔥 去除 `secrets.GITHUB_TOKEN` 配置方法
- 🔥 去除 `autoRelease` 和 `release` 徽章

## [1.1.0] - 2020-10-11

### ✨ 增加

- 🌐 完成 [README_EN.md](./README_EN.md)
- 📝 增加 [GitHub release (latest by date)](https://img.shields.io/github/v/release/yi-Xu-0100/hub-mirror) 的徽章
- 🍱 增加 [template](./template) 文件夹存放所有的模板

### ♻️ 变化

- 🚚 将原来的配置 [cache](./README.md#cache_path可选) 的 [使用示例](</yi-Xu-0100/hub-mirror/blob/v1.0.0/.github/workflows/sync2gitee(cached).yml>) 的名称由 `sync2gitee(cached).yml` 修改为 `sync2gitee.cached.yml`
- 🔧 将 [autoRelease](/yi-Xu-0100/hub-mirror/blob/v1.0.0/.github/workflows/autoRelease.yml) 中的运行任务名称由 `Auto Release` 改为 `Release`

### 🐛 修复

- 🐛 修复 GitHub page 无法渲染 `${{secrets.GITHUB_TOKEN}}` ，更改为 `secrets.GITHUB_TOKEN`

## [1.0.0] - 2020-09-19

### ✨ 增加

- 📝 完成 [README.md](./README.md)
- 📝 完成 [CHANGELOG.md](./CHANGELOG.md)
- 🔧 增加未配置 [cache](./README.md#cache_path可选) 的 [使用示例](./.github/workflows/sync2gitee.yml)
- 🔧 增加配置了 [cache](./README.md#cache_path可选) 的 [使用示例](<./.github/workflows/sync2gitee(cached).yml>)
- 👷 增加自动发布 release 的 [工作流](./.github/workflows/autoRelease.yml)

[unreleased]: https://github.com/olivierlacan/keep-a-changelog/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/mindsers/changelog-reader-action/compare/v1.0.0
[1.0.0]: https://github.com/mindsers/changelog-reader-action/compare/v1.0.0
