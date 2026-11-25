# File Explorer — User Manual

File Explorer is the native file manager and package installer included with MixtapeOS. It is available from the Info menu.

## Overview

File Explorer has two tabs:

- **FILES** — browse and manage the device filesystem;
- **APPS** — list, inspect and uninstall installed applications.

### FILES tab

The file tree starts at:

```text
/mnt/data
/mnt/system
```

Use the folder tree to navigate. The available actions are:

| Action | Description |
|---|---|
| **UP** | Go to the parent folder |
| **NEW** | Create a new folder |
| **RENAME** | Rename the selected item |
| **COPY** | Copy the selected item to the clipboard |
| **CUT** | Move the selected item to the clipboard |
| **PASTE** | Paste the clipboard into the current folder |
| **DELETE** | Delete the selected item after confirmation |
| **PERM** | Change Unix permissions, UID and GID where supported |
| **REFRESH** | Re-read the current folder |
| **INSTALL** | Install a selected `.archpkg` |
| **FW** | Open a selected `.archfw` firmware package |

File operations are confirmed before deletion and destructive actions. Permissions are meaningful on `/mnt/system`; `/mnt/data` is FAT-based, so Unix ownership and mode bits are not preserved there.

### APPS tab

The APPS tab shows installed applications from:

```text
/mnt/data/Apps/
```

Each entry shows the app name, package version and whether its Info-menu PDF exists. Apps can be removed with **UNINSTALL**, except File Explorer itself.

Uninstalling an app removes its application folder and its Info PDF.

### Installing an application

An application package uses the `.archpkg` format.

1. Copy the package to `/mnt/data`.
2. Open **FILES** in File Explorer.
3. Select the `.archpkg` file.
4. Choose **INSTALL** and confirm.
5. Wait for the installation page to complete.

The package installer:

- validates the archive and its checksums;
- rejects unsafe paths and symlinks;
- installs the payload under `/mnt/data/Apps/`;
- creates or updates the Info-menu PDF;
- writes a log to:

```text
/mnt/data/.archpkg_install.log
```

Do not power off during installation.

### Firmware updates

A MixtapeOS firmware package uses the `.archfw` format.

1. Copy the correct package to the device.
2. Open **FILES** and select the `.archfw` file.
3. Choose **FW**.
4. Review the version and target.
5. Select the components to install.
6. Choose **FULL UPDATE** or **ROOTFS**.
7. Press **UPDATE**.
8. Wait for completion.
9. Power off the device to apply the update on the next boot.

The package target is checked against the device:

- `flash` for the 605F;
- `hdd` for the 605 HDD.

A mismatch is rejected before any write.

A full update can include:

- rootfs;
- optfs;
- cpio;
- system files;
- data files.

The **ROOTFS** shortcut selects only the root filesystem.

### Firmware update safety

- Use the correct package for the device target.
- Do not power off during the update.
- Keep a recovery image and a backup of your data.
- Do not interrupt a rootfs write.
- Read the changelog before updating.

The updater writes temporary files, validates them and uses an atomic rename where supported. The final reboot is always manual: File Explorer does not reboot the device by itself.

## Related documentation

- [MTOS Settings manual](Manual_MTOSSET.md)
- [Mixtape DJ manual](Manual_MIXTAPEDJ.md)
- [Application packages](docs/24-app-packages.html)
- [MixtapeOS changelog](docs/28-mixtapeos.html)
