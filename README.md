**Minimal installer for Microsoft TrueType fonts on Linux Mint / Ubuntu**

This PPA provides a **lightweight version of `ttf-mscorefonts-installer`** that matches Debian’s upstream dependency policy. It avoids extra Ubuntu/Mint meta-packages that are **not required** for the fonts to install.

---

## Why this exists

* Ubuntu’s `ttf-mscorefonts-installer` depends on 8+ extra packages (update-manager, python3-distupgrade, ubuntu-advantage-tools, etc.)
* Debian’s upstream package only requires `wget`, `cabextract`, and `dpkg`
* This PPA rebuilds the Debian package **without unnecessary Ubuntu dependencies**, making installation cleaner and easier to maintain.

---

## How to use

### Add the PPA

```bash
sudo add-apt-repository ppa:seann-giffin/msttcorefonts-minimal
sudo apt update
```

### Pin the package (optional but recommended)

This ensures your system always prefers the minimal version:

1. Create `/etc/apt/preferences.d/msttcorefonts` with:

```text
Package: ttf-mscorefonts-installer
Pin: release o=LP-PPA-seann-giffin-msttcorefonts-minimal
Pin-Priority: 1001
```

2. Update APT:

```bash
sudo apt update
```

3. Verify:

```bash
apt-cache policy ttf-mscorefonts-installer
```

Your PPA version should appear as the candidate with the highest priority.

---

## License

* Packaging and installer scripts: **GNU GPL v2**
* Microsoft fonts are **downloaded at install time under Microsoft’s EULA** — see `/usr/share/doc/ttf-mscorefonts-installer/READ_ME!.gz` after installation.

---

## Notes

* This PPA only modifies the **dependencies**; the fonts themselves are unchanged.
* Safe for Linux Mint and Ubuntu systems.
* Fully compatible with existing font configurations.
