# How to Deploy JARVIS

This guide explains how to install Home Assistant, set up Hermes Agent, install Hermes Assist through HACS, and give Hermes access to your smart home.

## Step 1: Set Up Home Assistant

First, you need a working Home Assistant server.

When using Proxmox, follow:

```text
Guides/02_setting-up-hasos.md
```

If you already have Home Assistant installed, or if you prefer to install it without Proxmox, please follow the official Home Assistant installation guide instead. However, you will still need to complete Step 2 of the guide

## Step 2: Install Hermes Agent

Run the Hermes Agent installation script for your operating system.

### Linux

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

### Windows PowerShell

```powershell
irm https://hermes-agent.nousresearch.com/install.ps1 | iex
```

Follow the instructions shown by the installer.

During the integrations section, select **Home Assistant**.

You will need to enter:

* Your Home Assistant URL
* A Home Assistant long-lived access token

Your Home Assistant URL will normally look like:

```text
http://192.168.1.100:8123
```

Replace the IP address with the address of your own Home Assistant server.

## Step 3: Create a Long-Lived Access Token

In Home Assistant, click your profile in the bottom-left corner.

Open the **Security** section and scroll down to **Long-Lived Access Tokens**.

Click **Create Token**, give it a name such as:

```text
Hermes Agent
```

Copy the token and save it somewhere secure.

Home Assistant only shows the full token once.

Paste the token into the Hermes installer when it asks for your Home Assistant access token.

## Step 4: Configure the Hermes API Server

After Hermes is installed, open its configuration or run the Hermes setup command again.

Enable the Hermes API server and configure:

* The address on which the server should listen
* The API port
* An API key

When Hermes and Home Assistant are running on different machines, make sure the API listens on your network interface and not only on `localhost`.

Your Hermes API URL may look like:

```text
http://192.168.1.110:8000
```

The exact port depends on the port you selected in the Hermes configuration.

Create or copy the API key and save it somewhere secure. You will need both the API URL and API key when adding Hermes to Home Assistant.

Restart Hermes after changing its configuration.

## Step 5: Add the Hermes Assist Repository to HACS

Open your Home Assistant dashboard and click **HACS** in the sidebar.

When HACS does not appear, clear the browser cookies and cache for your Home Assistant address, reload the page, and try again.

Inside HACS, click the three dots in the upper-right corner and select **Custom repositories**.

Add:

```text
https://github.com/getthreadcontext/homey
```

Select **Integration** as the repository type and click **Add**.

Search for:

```text
Hermes Assist
```

Open it and click **Download**.

Wait until the integration has finished installing.

## Step 6: Restart Home Assistant

Go to **Settings** and click the restart notification shown at the top of the page.

Restart Home Assistant and wait for it to come back online.

## Step 7: Add the Hermes Integration

After Home Assistant has restarted, go to:

```text
Settings → Devices & services
```

Click **Add Integration** and search for:

```text
Hermes Agent
```

Enter:

* Your Hermes API URL
* The Hermes API key you created earlier

Uncheck:

```text
Ask Hermes Agent to create the Home Assistant skill
```

The skill was already configured through the Hermes installer, so it does not need to be created again.

Click **Submit**, and then click **Submit** again to complete the setup.

Home Assistant should now add the Hermes conversation agent.

## Step 8: Create a Voice Assistant

Go to:

```text
Settings → Voice assistants
```

Click **Add Assistant**.

Give the assistant a name, such as:

```text
JARVIS
```

For the conversation agent, select:

```text
Hermes Agent
```

Click **Create**.

You have now connected Hermes Agent to Home Assistant. Hermes can access your smart home, and you can chat with it through the Home Assistant Assist window.

## Step 9: Test Hermes With a Virtual Device

When you do not already have smart-home devices available for testing, I recommend using the **Virtual Devices** integration.

Open HACS and search for:

```text
Virtual Devices
```

Download the integration and restart Home Assistant.

After restarting, go to:

```text
Settings → Devices & services → Add Integration
```

Search for **Virtual Devices**, add it, and create a virtual device such as a light.

Open the Assist chat window in the upper-right corner of the Home Assistant dashboard.

Try a command such as:

```text
Turn on the virtual light.
```

Then try:

```text
Turn off the virtual light.
```

When Hermes correctly controls the device, the connection between Hermes Agent and Home Assistant is working.
