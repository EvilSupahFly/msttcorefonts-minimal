**Minimal installer for Microsoft TrueType fonts on Linux Mint / Ubuntu**

This PPA provides a **lightweight version of `ttf-mscorefonts-installer`** that matches Debian’s upstream dependency policy. It avoids extra Ubuntu/Mint meta-packages that are **not required** for the fonts to install.

---

## Why this exists

* Ubuntu’s `ttf-mscorefonts-installer` depends on 8+ extra packages (update-manager, python3-distupgrade, ubuntu-advantage-tools, etc.)
* Debian’s upstream package only requires `wget`, `cabextract`, and `dpkg`
* This PPA rebuilds the Debian package **without unnecessary Ubuntu dependencies**, making installation cleaner and easier to maintain.

---

## How to use

### Adding this PPA to your system
You can update your system with unsupported packages from this untrusted PPA by adding `ppa:seann-giffin/msttcorefonts-minimal` to your system's Software Sources. ([Read about installing](https://launchpad.net/+help-soyuz/ppa-sources-list.html))

```bash
sudo add-apt-repository ppa:seann-giffin/msttcorefonts-minimal
sudo apt update
```
        

For maximum compatibility, this project supports the following base Ubuntu versions and any derivatives (like Linux Mint) based on them:
 * bionic (18.04)
 * focal (20.04)
 * jammy (22.04)
 * noble (24.04)
 * questing (25.10)
 * resolute (26.04)
 
 
As such, this PPA can also be added to your system manually by copying the lines below and adding them to your system's software sources:

```text
deb https://ppa.launchpadcontent.net/seann-giffin/msttcorefonts-minimal/ubuntu YOUR_UBUNTU_VERSION_NAME_HERE main 
deb-src https://ppa.launchpadcontent.net/seann-giffin/msttcorefonts-minimal/ubuntu YOUR_UBUNTU_VERSION_NAME_HERE main
```


Signing key:
4096R/F1A0FE71AA98ACF3290D2FDA1111EE89C2D53117 ([What is this?](https://launchpad.net/+help-soyuz/ppa-sources-list.html))

Fingerprint:
F1A0FE71AA98ACF3290D2FDA1111EE89C2D53117


### Pinning the package (optional but recommended)

This ensures your system always prefers this `minimal` version:

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
