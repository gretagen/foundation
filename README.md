# Every wind turbine needs a tower.

This is the Haliade deployment and filesystem builder of haliade.

Single command: `tower`.


## Subcommands

- `tower place` : Bootstrap a Haliade system onto a drive using ZETA, install Limine, then run `chronos rewrite-limine`.
- `tower clone` : Legacy zstrappa behaviour: copy the whole live `/` into a partition.
- `tower deploy <dir>` : Deploy an Haliade root filesystem tree.
- `tower rebuild <dir>` : Build a bootable ISO from a root filesystem tree.
- `tower enable-generators <dir> [system|house] <name...>` — Enable nacelle generators in a root filesystem tree.
- `tower climb <dir> [shell]` : Enter a root filesystem tree with bubblewrap.

## Examples

```
tower place --uefi /dev/sda2 /dev/sda1
tower place --uefi /dev/sda2 /dev/sda1 /dev/sda3 --pass --init openrc
tower place --uefi /dev/sda2 /dev/sda1 --enable-generator merged_packages --config ./definition.lua
tower clone --uefi /dev/sda2 /dev/sda1
tower deploy ~/haliade-root
tower enable-generators ~/haliade-root system merged_packages
tower rebuild ~/haliade-root
tower climb ~/haliade-root
```

## Flags (place only)

- `--pass` : Do not ask for confirmation to bootstrap.
- `--init NAME` : Install an init of the user's choice (see ~/iniswap).
- `--config PATH` : Synchronize a Nacelle config into the deployed system.
- `--uefi` / `--bios` : Force bootloader mode.
