# OpenWRT-Repo
OpenWRT collective Repo of built packages of this account.

# Installation


## Adding the Custom Repo to an OpenWrt 25.12 Router

OpenWrt 25.12 uses the **`apk`** package manager (Alpine Package Keeper) instead of the legacy `opkg`. By default, it strictly enforces signature verification for all active repositories. Follow these steps to import the trusted public key and add the feed to your router.

### Step 1: Add the Public Signing Key
To allow your router to trust the signed packages, you must install the public key corresponding to the private key used in the GitHub Actions build pipeline.

1. Connect to your OpenWrt router via **SSH**.
2. Paste the contents of the public key into the file.

    ```
    echo '-----BEGIN PUBLIC KEY-----
    MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEcUlsK/z3CLqfZ5pafb1s9FCGfn4c
    RGCRcbUcwDl6fJLgstWmDAhbRnah/HnlHC3cKE2HS5lAEW2oP+YRvGV9tA==
    -----END PUBLIC KEY-----' >> /etc/apk/keys/custom_feed.pub
    ```

### Step 2: Register the Repository
Add the URL of your hosted GitHub Pages repository to the list of active package sources.


   ```
    echo 'https://g6094199.github.io/openwrt-repo/packages/"YOUR ARCH'/packages/packages.adb >> /etc/apk/repositories.d/customfeeds.list

   ```


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
