# ansible-paru

An Ansible module for installing [AUR](https://aur.archlinux.org/) packages via
the [paru][paru] AUR helper.

This assumes your target already has paru and its dependecies installed.

## Dependencies (Managed Node)

* [Arch Linux](https://www.archlinux.org/) (Obviously)
* [paru][paru]

## Installation

1. Clone this repo
2. Copy or link the `paru` file into your global Ansible library (usually
   `/usr/share/ansible`) or into the `./library` folder alongside your
   top-level playbook

## Usage

Pretty much identical to the [pacman module][pacman-mod]. Note that package
status, removal, the corresponding `pacman` commands are used (`-Q`, `-R`,
respectively).

### Options

| parameter    | required  | default | choices               | description                         |
|--------------|-----------|---------|-----------------------|-------------------------------------|
| name         | no        |         |                       | Name of the AUR package to install. |
| recurse      | no        | no      | yes/no                | Whether to recursively remove packages. See [pacman module docs][pacman-mod]. |
| state        | no        | no      | absent/present/latest | Whether the package needs to be installed or updated. |
| update_cache | no        | no      | yes/no                | Whether or not to refresh the master package lists. This can be run as part of a package installation or as a separate step. |
| upgrade      | no        | no      | yes/no                | Whether or not to upgrade the whole systemd. |

### Examples

```yaml
# Install package foo
- paru: name=foo state=present

# Ensure package fuzz is installed and up-to-date
- paru: name=fuzz state=latest

# Remove packages foo and bar
- paru: name=foo,bar state=absent

# Recursively remove package baz
- paru: name=baz state=absent recurse=yes

# Effectively run yay -Syu
- paru: update_cache=yes upgrade=yes
```

[paru]: https://github.com/Morganamilo/paru
[pacman-mod]: http://docs.ansible.com/pacman_module.html
