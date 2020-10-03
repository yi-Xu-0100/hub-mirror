## hub-mirror

[![sync2gitee](https://github.com/yi-Xu-0100/hub-mirror/workflows/sync2gitee/badge.svg)](./.github/workflows/sync2gitee.yml)
[![sync2gitee(cached)](<https://github.com/yi-Xu-0100/hub-mirror/workflows/sync2gitee(cached)/badge.svg>)](./.github/workflows/sync2gitee.cached.yml)
[![GitHub last commit](https://img.shields.io/github/last-commit/yi-Xu-0100/hub-mirror)](./)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/yi-Xu-0100/hub-mirror)](https://github.com/yi-Xu-0100/hub-mirror/releases)
[![LICENSE](https://img.shields.io/github/license/yi-Xu-0100/hub-mirror)](./LICENSE)

[English](./README_EN.md) | [简体中文](./README.md)

Template usage repository of [github action-hub-mirror-action](https://github.com/Yikun/hub-mirror-action), you can manage the mirror repositories actions between `GitHub` with other `hub`.

PS: This template repository only uses part of parameters configuring synchronization workflows. The parameters of `.github/workflows/sync2gitee.yml` need to be modified and configured by yourself to complete the personal workflows configuration.

## Table of Contents

- [hub-mirror](#hub-mirror)
- [Table of Contents](#table-of-contents)
- [Configuration parameter](#configuration-parameter)
  - [`src`(required)](#srcrequired)
  - [dst(required)](#dstrequired)
  - [`dst_key`(required)](#dst_keyrequired)
    - [Set `dst_key`](#set-dst_key)
  - [`dst_token`(required)](#dst_tokenrequired)
    - [Set `dst_token`](#set-dst_token)
  - [`static_list` (recommended)](#static_list-recommended)
- [Single repository usage](#single-repository-usage)
- [Thanks](#thanks)
- [LICENSE](#license)

## Configuration parameter

### `src`(required)

`src` is source account, such as `github/yi-Xu-0100`, is the `Github` account `yi-Xu-0100`.

![GitHub-Name](./static/github_name.png)

### dst(required)

`dst` is destination account, such as `gitee/yi-Xu-0100`, is the `Gitee` account `yi-Xu-0100`.

![Gitee-Name](./static/gitee_name.png)

### `dst_key`(required)

`dst_key` the `SSH` key to push code in destination account, You can get the `Github SSH key` in [here](https://github.com/settings/keys)，the `Gitee SSH key` in [here](https://gitee.com/profile/sshkeys).

#### Set `dst_key`

1. install `Git` and launch `GitBash`
2. Run the following command to generate an `SSH` key pair (The default configuration used by the picture, that is, skip all settings).

   ```sh
   ssh-keygen -t rsa
   ```

   ![Get SSH key pair](./static/rsa_gen.png)

3. According to the path obtained in the second step, add the key pair to the two libraries respectively (take `GitHub` and `Gitee` as examples)

   1. Add the private key (`id_rsa`) to the `GitHub` repository. Create a `GITEE_PRIVATE_KEY` variable through the `Secrets` in the `GitHub` **repository settings**, and copy the private key content to the value area.

      ![Add the private key](./static/add_secret_key.png)

   2. Add the public key (`id_rsa.pub`) to the `Gitee` repository. Create a `hub-mirror` variable through the `SSH Public Key` in the `Gitee` **personal settings**, and copy the public key content to the value area.

      ![Add the public key](./static/add_pub_key.png)

### `dst_token`(required)

`dst_token` is the `API` token to create non-existent repo. You can get `Github` token in [here](https://github.com/settings/tokens), and the `Gitee` in [here](https://gitee.com/profile/personal_access_tokens).

#### Set `dst_token`

Take `Gitee` as an example, get the token and add it to `GitHub`.

1. Generate a `GITEE_TOKEN` through `personal access token` in the `Gitee` **personal settings**, and copy the token content to the value area.

   PS: The token only appears once, please save it(it can be generated multiple times).

   ![Generate a personal access token](./static/secret_key.png)

2. Add the token to the `GitHub` repository, create a `GITEE_TOKEN` variable through the `Secrets` in the `GitHub` **repository settings**, and copy the private key content to the value area.

   ![Add the token](./static/secret_key_1.png)

### `static_list` (recommended)

`static_list` is repos only mirror, but don't get list from repo api dynamically (the white/black list is still available), like 'repo1,repo2,repo3'. The `${{ github.event.repository.name }}` used by `static_list` in the template repository only specifies the current repository (ie, the template repository). At the same time, you need to pay attention to the following issues when setting the repository name:

- Pay attention to the case and symbols of the repository name.
- The current action `hub-mirror-action@v0.09` will synchronize all repositories and create all repositories cloned under `GitHub` in another `hub`.
- The current action `hub-mirror-action@v0.09` **can not complete** the mirror synchronization for the private repository, it may interrupt the synchronization process and cause some repositories to not be synchronized.

## Single repository usage

Because `static_list` only sets the current repository, you can choose to place `.github/workflows/sync2gitee.yml` in the **same path** of any repository without adding the parameters, to realize the configuration of synchronizing only the repository containing the file.

PS: You also need [Configuration Parameters](#configuration-parameter).

## Thanks

- [Yikun/hub-mirror-action](https://github.com/Yikun/hub-mirror-action)
- [ShixiangWang/sync2gitee](https://github.com/ShixiangWang/sync2gitee)

## LICENSE

[MIT](./LICENSE)
