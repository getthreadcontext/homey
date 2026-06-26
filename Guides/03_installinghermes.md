# Setting Up Hermes Agent

Hermes Agent can also be installed using a Proxmox community script. However, I recommend installing it manually.

Installing it manually teaches you how to create a container, configure its resources and network, and properly set up Hermes Agent.

## Step 1: Download a Debian Container Template

Open the Proxmox web interface and select your **pve** server.

Under the server, click **local** storage and open **CT Templates**.

Click **Templates**, search for the latest standard Debian template, and download it.

Wait for the download to finish.

## Step 2: Create the Container

Click **Create CT** in the upper-right corner of the Proxmox web interface.

Enter the basic container information:

* **Hostname:** hermes
* **Password:** Choose a secure password
* **Unprivileged container:** Enabled

Click **Next** and select the Debian template you downloaded.

For the resources, I used:

* **Disk:** 16 GB
* **CPU cores:** 4
* **Memory:** 4 GB
* **Swap:** 1 GB

You can change these settings later if Hermes needs more resources.

## Step 3: Configure the Network

For the network bridge, select:

```text
vmbr0
```

Set IPv4 to **DHCP** so the container automatically receives an IP address from your router.

The other default network settings should normally be fine.

Continue through the setup pages, check the settings, and click **Finish**.

## Step 4: Start the Container

Select the new **hermes** container under **pve**.

Click **Start** and then open **Console**.

Log in with:

```text
Username: root
Password: The password you selected when creating the container
```

## Step 5: Update Debian

Update the container before installing Hermes:

```bash
apt update && apt upgrade -y
```

Install `curl`:

```bash
apt install curl -y
```

## Step 6: Install Hermes Agent

Run the Hermes Agent installer:

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

Wait for the installer to download Hermes and install everything it needs.

During the setup, select the AI provider you want to use and enter an API key when required.

After the installation has finished, start Hermes using:

```bash
hermes
```

You should now be able to talk to Hermes Agent from the container console.

Hermes is now installed and ready to be connected to the other parts of the JARVIS project.
