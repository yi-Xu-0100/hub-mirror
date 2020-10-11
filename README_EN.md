## hub-mirror

[![sync2gitee](https://github.com/yi-Xu-0100/hub-mirror/workflows/sync2gitee/badge.svg)](./.github/workflows/sync2gitee.yml)
[![sync2gitee(cached)](<https://github.com/yi-Xu-0100/hub-mirror/workflows/sync2gitee(cached)/badge.svg>)](./.github/workflows/sync2gitee.cached.yml)
[![GitHub last commit](https://img.shields.io/github/last-commit/yi-Xu-0100/hub-mirror)](./)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/yi-Xu-0100/hub-mirror)](https://github.com/yi-Xu-0100/hub-mirror/releases)
[![LICENSE](https://img.shields.io/github/license/yi-Xu-0100/hub-mirror)](./LICENSE)

[English](./README_EN.md) | [简体中文](./README.md)

Template usage repository of [GitHub action-hub-mirror-action](https://github.com/Yikun/hub-mirror-action), you can manage the mirror repositories actions between `GitHub` with other `hub`(only `Gitee` now).

**PS: This template repository only uses part of parameters configuring synchronization workflows. The parameters of usage examples in [`template`](./template) need to be modified and configured by yourself to complete the personal workflows configuration.**

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
  - [`acount_type` (recommended)](#acount_type-recommended)
  - [`force_update` (recommended)](#force_update-recommended)
  - [`cache_path` (optional)](#cache_path-optional)
- [Single repository usage](#single-repository-usage)
- [FAQ](#faq)
  - [`Gitee` can't create `XXX` repository and how to solve it](#gitee-cant-create-xxx-repository-and-how-to-solve-it)
  - [`actions/cache' configuration](#actionscache-configuration)
  - [`secrets.GITHUB_TOKEN` configuration](#secretsgithub_token-configuration)
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

`static_list` is repos only mirror, but don't get list from repo api dynamically (the white/black list is still available), like `'repo1,repo2,repo3'`. The `static_list` in the template contains only the current repository (ie template repository) as obtained from [`actions/github-script`](https://github.com/actions/github-script). If you need to add or modify it, use comma separations, such as: `'${{ steps.info.outputs.result }},MY_REPO'` . Also, when setting the name of the repository, the following issues need to be considered:

- Pay attention to the case and symbols of the repository name.
- The current action `hub-mirror-action@v0.09` will synchronize all repositories and create all repositories cloned under `GitHub` in another `hub`(`Gitee` would not show the relation about clone).
- The current action `hub-mirror-action@v0.09` **can not complete** the mirror synchronization for the private repository, it may interrupt the synchronization process and result that some repositories to not be synchronized.

### `acount_type` (recommended)

`account_type` configures the user attributes that use this workflow.

- If it is an individual, it needs to be set to `user`.
- If it is an organization, it needs to be set to `org`.

### `force_update` (recommended)

`force_update` configures whether or not to force synchronization. This option is used when there is a conflict between the contents of the `GitHub` and `Gitee` repositories.

- If configured as `true`, the `GitHub` repository content is forced to be pushed into `Gitee`.
- If it is configured as `false`, it will not force the `GitHub` repository content to be pushed to `Gitee`.

### `cache_path` (optional)

**Note: Improperly configured `cache` will still cause the entire repository to take too long to synchronize. See [`actions/cache` configuration](#actionscache-configuration) for detailed configuration.**

The `cache_path` option needs to be used with [`actions/cache`](https://github.com/actions/cache), which will cache the synchronized repository contents and shorten the synchronization time.

- [`sync2gitee.cache.yml`](./.github/workflows/sync2gitee(cached).yml) is an example of using `cache_path` configured.
- [`sync2gitee.yml`](./template/sync2gitee.yml) is a using case where `cache_path` is not configured.

## Single repository usage

Because `static_list` only sets the current repository, you can choose to place `.github/workflows/sync2gitee.yml` in the **same path** of any repository without adding the parameters, to realize the configuration of synchronizing only the repository containing the file.

PS: You also need [Configuration Parameters](#configuration-parameter).

## FAQ

### `Gitee` can't create `XXX` repository and how to solve it

`Gitee` repository name creation requirements: Only letters, numbers, or underscores(`_`), Dash(`-`), periods ( `.` ). **It must begin with a letter** and be 2~191 characters long. If your repository name begins with special symbols and numbers, it will interrupt the creation process and cause synchronization to fail.

Solution:

1. Repositories can be imported directly from `GitHub` using the service provided by `Gitee`, see [Gitee Help Manual](https://gitee.com/help/articles/4261), which also requires that only letters, numbers, underscores(`_`), dash(`-`) and periods(`.`). **It must begin with a letter or number**.
2. if the repository name begins with a special symbol, you can use [renaming a repository](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/renaming-a-repository) or [deleting a repository](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/deleting-a-repository) and [creating a repository on github](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github).

### `actions/cache' configuration

The synchronization process in the repository uses the action `actions/cache` to complete the caching of the repository. The setup of the synchronization repository in template is already done, so **no changes** are needed. In order to complete the cache configuration, and to build the parameters needed for `key`, we use **three steps** to complete the `cache` configuration, as shown in [`template/sync2gitee.cache.yaml`](./template/sync2gitee.cached.yaml).

```yaml
- name: Get current repository name
  id: info
  uses: actions/github-script@v3.0.0
  with:
    github-token: ${{secrets.GITHUB_TOKEN}}
    result-encoding: string
    script: |
      core.setOutput('date', new Date(Date.now()).toISOString().replace(/[^0-9]/g, ""))
      return context.repo.repo;

- name: Cache src repos
  uses: actions/cache@v2.1.1
  id: cache
  with:
    path: ${{ github.workspace }}/hub-mirror-cache
    key: ${{ runner.os }}-${{ github.repository_owner }}-${{ steps.info.outputs.result }}-cache-${{ steps.info.outputs.date }}
    restore-keys: ${{ runner.os }}-${{ github.repository_owner }}-${{ steps.info.outputs.result }}-cache-
```

Explanation:

- The step which `id` is`info` uses `actions/github-script` to get the repository name (also used for the [`static_list` configuration](#static_list-recommended)) and the trigger timestamp (`ISO` format and numbers only).
- The `path` variable sets the path corresponding to the path set by the parameter `cache_path` in `hub-mirror-action` (no change is recommended, the currently configured directory is the default value for the parameter configuration).
- `key` variable configuration is related to the environment, repository owner and repository name, and a trigger timestamp to determine specificity (the information is already available through the process steps, it is recommended not to change it).
- `restore-keys` matches only the preexisting keywords, which guarantees that the most recent cached result will be retrieved each time.
- `key` deletes the old cache file if it has not been triggered for `7` days or if the cached result store size is larger than `5G`.
- Detailed instructions for configuring `cache` can be found in the [`cache` repository documentation](https://github.com/actions/cache).

### `secrets.GITHUB_TOKEN` configuration

**This parameter is no need to configured and is automatically created and retrieved by `GitHub`.**

Reference: [Authentication in Workflow](https://docs.github.com/en/free-pro-team@latest/actions/reference/authentication-in-a-workflow)

## Thanks

- [ShixiangWang/sync2gitee](https://github.com/ShixiangWang/sync2gitee)
- [Yikun/hub-mirror-action](https://github.com/Yikun/hub-mirror-action)
- [actions/checkout](https://github.com/actions/checkout)
- [actions/cache](https://github.com/actions/cache)
- [actions/github-script](https://github.com/actions/github-script)

## LICENSE

[MIT](./LICENSE)
