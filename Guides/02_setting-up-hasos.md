# Install Home Assistant OS and Everything We Need

First, we will install **Home Assistant OS**.

We could install everything manually, but luckily there are community scripts that can automatically set everything up for us.

## Step 1: Install Home Assistant OS

Open the shell in Proxmox.

You can do this by clicking **pve** under **Datacenter**, and then clicking **Shell** in the right-side menu.

Paste this command into the shell:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/vm/haos-vm.sh)"
```

Select **Yes** and use the default settings.

You can change the settings later, but the defaults are fine for now.

Wait while Home Assistant OS installs.

When it is finished, open the new **HAOS** virtual machine under **pve** and click **Console**.

Wait for Home Assistant to start.

After it has started, open this address in your browser:

```text
http://VM-IP:8123
```

You can find the virtual machine's IP address under **Summary**.

Follow the Home Assistant setup process. After the setup is complete, you will be brought to the Home Assistant homepage.

# Step 2: Install HACS

In the bottom-left corner of Home Assistant, click **Settings**.

Then go to:

**Apps → App Store**

Click the three dots in the upper-right corner and select **Repositories**.

Add this repository:

```text
https://github.com/hacs/addons
```

Install the HACS app and start it.

After starting it, go back to **Settings**, click the three dots in the upper-right corner, and restart Home Assistant.

Wait for Home Assistant to finish restarting.

After that, clear your browser cache and go to **Devices & Services**.

Click **Add Integration** and search for **HACS**.

Follow the HACS setup process.

Well done! You have now set up Home Assistant OS and HACS.
