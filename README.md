# msttcorefonts-minimal PPA

This PPA provides a **minimal, Debian-derived build** of `ttf-mscorefonts-installer` (source package: `msttcorefonts`) for Ubuntu and Linux Mint.

## Why this PPA exists

On Ubuntu (and therefore Linux Mint), the stock `ttf-mscorefonts-installer` package pulls in a large set of **unrelated system-management dependencies**, including:

* `update-manager`
* `ubuntu-release-upgrader`
* `ubuntu-advantage-tools`
* Python helpers used only by Ubuntu's update stack

None of these are required to:

* download the Microsoft core fonts
* install them
* use them at runtime

Debian's upstream package correctly depends only on what is actually needed (`cabextract`, `wget`, `dpkg`).

This PPA simply:

* tracks the **Debian `msttcorefonts` package**
* rebuilds it for Ubuntu releases
* **does not add Ubuntu's extra meta-dependencies**

No functionality is removed.
Only unnecessary dependencies are avoided.

---

## Supported releases

This PPA publishes builds for the following Ubuntu series:

* 18.04 (bionic)
* 20.04 (focal)
* 22.04 (jammy)
* 24.04 (noble)
* newer series as available

Linux Mint users are supported **via Mint's Ubuntu base**.

---

## Installation (Linux Mint & Ubuntu)

> **Important (Mint users):**
> Do **not** use `add-apt-repository`.
> It uses Mint codenames and legacy key handling, which will break this PPA.

### 1. Import the PPA signing key (modern keyring method)

```bash
sudo mkdir -p /etc/apt/keyrings

curl -fsSL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0xF1A0FE71AA98ACF3290D2FDA1111EE89C2D53117" \
| sudo gpg --dearmor -o /etc/apt/keyrings/msttcorefonts-minimal.gpg

sudo chmod 644 /etc/apt/keyrings/msttcorefonts-minimal.gpg
```

---

### 2. Add the repository (Mint-safe)

```bash
echo "deb [signed-by=/etc/apt/keyrings/msttcorefonts-minimal.gpg] \
https://ppa.launchpadcontent.net/seann-giffin/msttcorefonts-minimal/ubuntu \
$(. /etc/os-release && echo $UBUNTU_CODENAME) main" \
| sudo tee /etc/apt/sources.list.d/msttcorefonts-minimal.list
```

This uses the **Ubuntu base codename**, not the Mint codename, as this PPA follows Ubuntu's release naming scheme.

---

### 3. Update and install

```bash
sudo apt update
sudo apt install ttf-mscorefonts-installer
```

> The `msttcorefonts` name is provided as a virtual package; installing either name will correctly resolve to `ttf-mscorefonts-installer`.

---

## Verifying that the minimal package is in use

You can confirm that APT is selecting the PPA version:

```bash
apt-cache policy ttf-mscorefonts-installer
```

The installed and candidate versions should come from:

```
ppa.launchpadcontent.net/seann-giffin/msttcorefonts-minimal
```

### Package Installation Note
> This PPA installs the `msttcorefonts` package directly (as produced upstream by Debian) and nothing else.
> The Ubuntu transitional name `ttf-mscorefonts-installer` is intentionally not used as it would conflict with Ubuntu's own meta-package.

---

## Troubleshooting

### `NO_PUBKEY 1111EE89C2D53117`

This means the repository exists but the signing key is not correctly bound.

Fix by re-importing the key:

```bash
sudo rm -f /etc/apt/keyrings/msttcorefonts-minimal.gpg

curl -fsSL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x1111EE89C2D53117" \
| sudo gpg --dearmor -o /etc/apt/keyrings/msttcorefonts-minimal.gpg

sudo chmod 644 /etc/apt/keyrings/msttcorefonts-minimal.gpg
sudo apt update
```

Also ensure there is **only one** source entry for this PPA:

```bash
grep -R "msttcorefonts-minimal" /etc/apt/sources.list /etc/apt/sources.list.d/
```

Remove duplicates like this:

```bash
sudo rm -f </full/path/to/duplicate_file_name.list>
```

---

### `add-apt-repository` fails or installs the Ubuntu version

This is expected on Linux Mint.
Remove any auto-generated files and follow the manual instructions above.

---

## Licensing

* Packaging scripts and installer logic: **GPL-2.0-or-later**
* Fonts themselves: **Microsoft license** (downloaded by the installer)

This matches Debian's licensing and packaging policy.

---

## Maintenance policy

* Tracks Debian's `msttcorefonts` package from `unstable`
* Rebuilds only when Debian updates
* No Ubuntu-specific patches are added

This PPA is intentionally boring but still uses APT's Super COW Powers.
