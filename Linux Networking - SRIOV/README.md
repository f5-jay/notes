# SRIOV

Useful Resources
- https://www.reddit.com/r/VFIO/comments/tqhld9/iommu_sriovnoob_understanding_why_pciassignbusses/
- https://lenovopress.lenovo.com/lp1467.pdf
- https://gist.github.com/mcastelino/08f6e49f2faba295eb690a3a8ee44c70

IOMMU (Input-Output Memory Management Unit)

Requires VT-d to be enabled in the BIOS and explicitly enabled in the Linux Kernel. To do so, pass either intel_iommu=on (for Intel systems) or amd_iommu=on (for AMD systems) added to the kernel command line. In addition it is recommended to use iommu=pt option which improves IO performance for devices in the host.

Once the system boots up, check the contents of /sys/kernel/iommu_groups/ directory. 


To determine if the system CPU architecture is Intel or AMD:

```
lscpu
```

Add either GRUB option (depending on CPU architecture to GRUB_CMDLINE_LINUX_DEFAULT:

```
intel_iommu=on  
```
```
amd_iommu=on
```

OTHER OPTIONS:

```
iommu=pt
```
NOTE: iommu=pt turns on iommu tagging only for devices configured for pass through, allowing the host to ignore it for local host-only devices. 

```
pcie_acs_override=downstream
```
NOTE: Splits the NIC into two

```
ixgbe.max_vfs=16 
pci=realloc,assign-busses,nocrs
```

```
dmesg | grep -i iommu
```

```
dmesg | grep 'IOMMU enabled'
```

To determin if IOMMU is enabled:

```
dmesg | grep -e DMAR -e IOMMU
```


To Identify all IOMMU Groups (run as root):
```
for d in $(find /sys/kernel/iommu_groups/ -type l | sort -n -k5 -t/); do n=${d#*/iommu_groups/*}; n=${n%%/*}; printf 'IOMMU Group %s ' "$n"; lspci -nns "${d##*/}"; done;
```

Hereby driver kvm maps to "kernel_irqchip=on" and driver qemu maps to "kernel_irqchip=split".

```
 <features>
   <ioapic driver='kvm'/>
 </features>
```
```
  <qemu:commandline>
    <qemu:arg value='-device'/>
    <qemu:arg value='intel-iommu'/>
    <qemu:arg value='intremap=on' />
    <qemu:arg value='caching=on' />
  </qemu:commandline>
```

```
  <features>
    <ioapic driver="qemu"/>
  </features>
```
```
    <iommu model="intel">
      <driver intremap="on" caching_mode="on" eim="on"/>
    </iommu>
```
