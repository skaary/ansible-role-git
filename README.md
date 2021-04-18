# Ansible Role: Git
[![CI](https://github.com/skaary/ansible-role-git/actions/workflows/ci.yml/badge.svg?branch=main&event=push)](https://github.com/skaary/ansible-role-git/actions?query=workflow%3Ci)

An Ansible Role that installs [Git](https://git-scm.com/) and configures the global gitconfig and gitignore on Linux.

Gitconfig can be configured either system-wide (`/etc/gitconfig`) or per user (`home/{{ git_user }}/.config/git/config`).

## Requirements

None

## Role Variables

| Variable name                 | Default value | Description |
|-------------------------------|---------------|-------------|
| `git_user`                     | `{{ ansible_user_id }}`            | The name of the user to install the git role for. Required. |
| `git_packages`                     | `git`            | The git packages to be installed. Required. |
| `gitconfig_set`          | `true` | Conditional for using/not using (`true`/`false`) git configuration settings/template. Required. |
| `gitignore_set`          | `true` | Conditional for using/not using (`true`/`false`) git ignore settings/template. Required. |
| `gitconfig_set_commit_message`          | `false` | Conditional for using/not using (`true`/`false`) a custom commit message/template. Required. |
| `git_path`          | `/home/{{ git_user }}/.config/git` | The default location for git configuration files. Required.|
| `gitconfig_path`          | `{{ git_path }}/config` | The default location for gitconfig file. Required |
| `gitignore_path`          | `{{ git_path }}/ignore` | The default location for gitignore file. Required |
| `gitconfig_commit_message_path`          | `{{ git_path }}/message` | The default location for a custom git ignore message. Required. |
| `gitconfig_alias`          | `""` | Variable for `[alias]` section in gitconfig. |
| `gitconfig_color`          | `""` | Variable for `[color]` section in gitconfig. |
| `gitconfig_core`          | `""` | Variable for `[core]` section in gitconfig. |
| `gitconfig_diff`          | `""` | Variable for `[diff]` section in gitconfig. |
| `gitconfig_user`          | `""` | Variable for `[user]` section in gitconfig. |
| `gitconfig_commit`          | `template: "{{ gitconfig_commit_message_path }}` | Variable for `[commit]` section in gitconfig. |
| `gitconfig_other`          | `""` | Variable for undefined sections in the gitconfig template. See Example Playbook. |
| `gitignore`          | `""` | Variable for adding intentionally untracked files that Git should ignore to gitignore. |

## Example Playbook

### Configure system /etc/gitconfig

Set `git_user: system` for write to `/etc/gitconfig`:

```yaml
hosts: all
vars:
  git_user: system
  gitconfig_color:
    ui: auto
  gitconfig_other:
    github:
      user: user
      email: user@email.com
roles:
  - git
```

### Configure user ~/.config/git/config and ~/.config/git/ignore

Default `git_user` set to `ansible_user_id`:

```yaml
hosts: all
vars:
  git_config_color:
    ui: auto
  gitignore:
    - ".idea"
roles:
  - git
```

## License
