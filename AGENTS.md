# AMD R600 issue on 1st pci-e slot on U4 CPC945 Power Mac G5

Identified root cause: this is Bug 95015 (2016), affecting all r600+ (TeraScale) AMD GPUs (Caicos, Cedar, Turks, Cayman) on the U4 x16 PCIe slot. The x8 slot works.
The 32-bit DMA quirk (dart_1st_pcie_slot.patch) was written for Cedar on POWER8/9 servers (commit 2c83029cda55), not for Mac G5, and doesn't fix the U4 x16 issue.
U4 DART bypass gives DMA addresses in phys + 0x8000000000 (~39 bits). Even Cayman (40-bit MC) fails, proving it's not an address-width problem.
The U4 bypass path has a fundamental incompatibility with how r600+ GPUs handle PCIe DMA transactions – likely a snoop/ordering issue.
Created patch 0009-u4-dart-bypass-fix.patch to raise the bypass DMA mask threshold for display-class devices from 40 to 64 bits, forcing them to use the DART IOMMU instead (same path the x8 slot uses, which works).

# What user tried so far
swiotlb=force pcie_aspm=off pci=pcie_bus_safe
all of them gives ring 0 GPU hardware acceleration disabled
user tried pcie_aspm=off pci=pcie_bus_safe beucase he compared lspci -vvv -s for the bios of a geforce 6600 with a mac vbios that works on that slot pci-e x16 and what differs when using the radeon 0000:0a:00.0 with a PC vbios
Critical difference:
GeForce 6600: ASPM Disabled, MaxReadReq 128 bytes
Radeon CAICOS: ASPM L0s L1 Enabled, MaxReadReq **512 bytes**
User suspected too that there was an issue with DMA of 40-bit vs 32-bit on AMD CAICOS that could fail on IBM powerpc devices, tried to use a mask to make the GPU fall to 32-bit on dma but it seems didn't work and may not be the root cause.

# Need user to maybe try
radeon.agpmode=-1, radeon.msi=0, or pci=nomsi

# There's ring5 UVD3.1 fail too to fix

User has a CI build and compiles via github actions workflow with PKGBUILD
There's linux 7.1.1 source clone located at /run/media/orestes/Guinea_pig/Projetos/linux/


If 128 doesn't fix it, it's not a pure read-size problem. Next steps in order:

Try 64 bytes — drop the limit further (pcie_set_readrq(rdev->pdev, 64))
Try pci=nomsi — MSI from Caicos may not complete correctly on U4; forced INTx avoids that path
Clear RlxdOrd (Relaxed Ordering) in DevCtl — GeForce 6600 may not set this; if the U4 reorders completions the CP can hang
Add a U4-specific quirk in arch/powerpc/platforms/powermac/pci.c to rewrite DevCtl of any downstream device to conservative settings (MaxReadReq=128, RlxdOrd=0, NoSnoop=0, RCB=128)
The x8 slot working strongly suggests the U4 can handle this GPU — just not with the x16 slot's bridge topology/configuration. If all software workarounds fail, it's likely a U4 hardware erratum specific to x16 electrical configuration, and the x8 slot is the practical fix.
