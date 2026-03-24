# pve9-dg1-passthrough

DG1 PCIE reset 命令存在问题，需要在内核层补丁拦截发给它的reset

DG1 固件中cfg区存在越界问题，硬编码 `cfg_size = PCI_CFG_SPACE_SIZE`

确认在[pve-kernel](https://git.proxmox.com/git/pve-kernel.git) commit `11cf9f46a056106a22078afc75612d25fb0e553d` 可用

将patch放到`pve-kernel/patches/kernel`目录，然后重新`make`即可

## 已知问题

1. 启动后似乎会导致对应虚拟机控制台无法启动，报错 `VM 100 qmp command 'set_password' failed - Could not set password TASK ERROR: Failed to run vncproxy`，不影响别的虚拟机

1. 如果遇到DG1卡住，需要重启PVE
