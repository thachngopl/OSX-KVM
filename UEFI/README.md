### Setting up UEFI enabled macOS

**This is under development. No support is provided for OVMF and Clover based
installations at the moment. Experiment at your own risk.**

* Install macOS by following the usual Enoch method.

* Build and use QEMU from https://github.com/kholia/qemu/. Use the "macOS"
  branch. Clover + macOS will fail to boot without this step.

* Install the included `Clover_v2*.pkg` on the main macOS disk.

  * Hit the `Customize` button during Clover install.

  * Tick 'Install for UEFI booting only', OsxAptioFix2Drv-64 and
    PartitionDxe-64 options.

* The Clover installer should leave the EFI partition mounted for us. Open that
  up in Finder.

  * Replace the `EFI/CLOVER/config.plist` file with `config.plist` included in
    this folder.

  * Put the included `q35-acpi-dsdt.aml` file into `EFI/CLOVER/ACPI/origin`
    location.

* You may edit `EFI/CLOVER/config.plist` to change the screen resolution from
  `800x600` to a higher **supported** value.

  This change also requires a corresponding change in the OVMF settings. When
  using OVMF with a virtual display (without VGA passthrough), you can set the
  client resolution in the OVMF menu, which you can reach with a press of the
  ESC button during the OVMF boot logo.

* Finally, use `boot-clover.sh` to use OVMF/UEFI to boot macOS with Clover.

* You can use `Clover Configurator` to modify your Clover configuration, if
  required.

#### Credits

* Nicholas Sherlock and others - UEFI, Clover, and other hacks

* Kyle Dayton - UEFI, Clover, and GPU passthrough notes

* https://pve.proxmox.com/wiki/Qemu/KVM_Virtual_Machines

* https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF
