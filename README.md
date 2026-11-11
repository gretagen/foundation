# Every wind turbine needs a tower.

This is the Haliade deployment and filesystem builder of haliade.

Single command: `tower`.


## Subcommands

- `tower place` : Bootstrap a Haliade system onto a drive using ZETA, install Limine, then run `chronos rewrite-limine`.
- `tower clone` : Legacy zstrappa behaviour: copy the whole live `/` into a partition.
- `tower deploy <dir>` : Deploy an Haliade root filesystem tree (usr-merge layout, host thesh config, default root shell; re-running heals an existing tree).
- `tower rebuild <dir>` : Build a bootable ISO from a root filesystem tree.
- `tower enable-generators <dir> [system|house] <name...>` — Enable nacelle generators in a root filesystem tree.
- `tower climb <dir> [shell]` : Enter a root filesystem tree with bubblewrap. Default shell: the tree root's login shell (from its `/etc/passwd`), else thesh.

## Examples

```
tower place --uefi /dev/sda2 /dev/sda1
tower place --uefi /dev/sda2 /dev/sda1 /dev/sda3 --pass --init openrc
tower place --uefi /dev/sda2 /dev/sda1 --enable-generator merged_packages --config ./definition.lua
tower clone --uefi /dev/sda2 /dev/sda1
tower deploy ~/haliade-root
tower deploy ~/haliade-root --pass --shell bash
tower enable-generators ~/haliade-root system merged_packages
tower rebuild ~/haliade-root
tower climb ~/haliade-root
```

## Flags (place and deploy)

- `--pass` : Do not ask for confirmation to bootstrap.
- `--shell NAME` : Default root shell written into the tree's `/etc/passwd` (default: `thesh`). `tower climb` honours it.
- `--config PATH` : Synchronize a Nacelle config into the deployed system.
- `--enable-generator NAME` / `--enable-house-generator NAME` : Enable nacelle generators (repeatable).
- `--system-generators-file PATH` / `--house-generators-file PATH` : Copy a generators file into the deployed system.

## Flags (place only)

- `--init NAME` : Install an init of the user's choice (see ~/iniswap).
- `--uefi` / `--bios` : Force bootloader mode.
