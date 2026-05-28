# OpenWRT-feed-collection
OpenWRT collective feeds of built packages of this account.

# Installation


## Adding the Custom Feed to an OpenWrt 25.12 Router

OpenWrt 25.12 uses the **`apk`** package manager (Alpine Package Keeper) instead of the legacy `opkg`. By default, it strictly enforces signature verification for all active repositories. Follow these steps to import the trusted public key and add the feed to your router.

### Step 1: Add the Public Signing Key
To allow your router to trust the signed packages, you must install the public key corresponding to the private key used in the GitHub Actions build pipeline.

1. Connect to your OpenWrt router via **SSH**.
2. Create and open a new key file:
   ```bash
   vi /etc/apk/keys/custom_feed.pub
   ```
3. Paste the contents of the public key into this file, then save and exit (`:wq`).

    ```
    -----BEGIN PUBLIC KEY-----
    MCowBQYDK2VwAyEAPwftG6AI2MuawR7Q7bFJU0CZ6R+2I9/E7oLdrv6jLi4=
    -----END PUBLIC KEY-----
    ```

### Step 2: Register the Feed Repository
Add the URL of your hosted GitHub Pages repository to the list of active package sources.

1. Open the repositories configuration file:
   ```bash
   vi /etc/apk/repositories
   ```
2. Append the following line at the very end of the file:
   ```text
   https://g6094199.github.io/OpenWRT-feed-collection/packages/noarch
   ```
3. Save and close the file.

---

### Step 3: Update and Install Packages
Refresh the local package index to fetch metadata from the new feed and install your tool.

```bash
# Update the package lists
apk update

# Install the package
apk add wg-friendly
```

If everything is configured correctly, `apk` will fetch and install the tool seamlessly without throwing any untrusted signature warnings.
