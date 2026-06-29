# Adding a Face to JARVIS

In this step, I will turn my old Echo Show into a self-hosted smart display and voice device for JARVIS.

I will use **View Assist** together with the **VACA View Assist Companion App**.

The Echo Show will work as both:

* A screen for JARVIS
* A smart-home dashboard
* A voice-assistant device
* A microphone and speaker for Home Assistant
* A way to talk to JARVIS using a wake word

This means I can say a wake word such as **Hey Jarvis**, ask a question or give a command, and get both a spoken and visual response.

## Before Starting

Your Echo Show needs to be unlocked and running an Android-based operating system such as LineageOS.

This guide assumes that the Echo Show can already:

* Connect to Wi-Fi
* Install Android APK files
* Open a web browser
* Access your Home Assistant server

The Echo Show and Home Assistant should be connected to the same network.

## Step 1: Install View Assist

First, install View Assist in Home Assistant.

Open **HACS** and search for:

```text
View Assist
```

Install the integration and restart Home Assistant when asked.

After Home Assistant has restarted, go to:

```text
Settings → Devices & services → Add integration
```

Search for **View Assist** and follow the setup process.

View Assist will be responsible for showing visual information from the voice assistant, changing views, displaying responses, and controlling what appears on the Echo Show.

## Step 2: Install the VACA Integration

Open HACS again and add the VACA repository as a custom repository if it is not already available.

Use this repository:

```text
https://github.com/msp1974/ViewAssist_Companion_App
```

Select **Integration** as the repository type.

Install the VACA integration and restart Home Assistant.

After restarting, go to:

```text
Settings → Devices & services → Add integration
```

Search for **VACA** and add the integration.

## Step 3: Install the VACA App on the Echo Show

Download the latest VACA APK from the View Assist Companion App GitHub releases page.

Move the APK file to the Echo Show or download it directly on the device.

Open the APK and install it.

Android may ask you to allow installation from unknown sources. Enable this permission for the browser or file manager you are using.

After the installation is complete, open the VACA app.

## Step 4: Connect VACA to Home Assistant

Inside the VACA app, enter the address of your Home Assistant server.

For example:

```text
http://192.168.1.100:8123
```

Use the real IP address of your Home Assistant server.

Log in with your Home Assistant account and allow the requested permissions.

The app may request access to:

* The microphone
* The speaker
* The camera
* Notifications
* Running in the background

Allow the permissions needed for the voice assistant and display features.

After connecting, the Echo Show should appear as a new device in Home Assistant.

## Step 5: Select the Hermes Voice Assistant

Open Home Assistant and go to:

```text
Settings → Voice assistants
```

Make sure you already have a working voice pipeline using:

* Hermes conversation agent
* Hermes speech-to-text
* Hermes text-to-speech

Open the VACA device settings and select this voice-assistant pipeline.

This connects the Echo Show to Hermes Agent through Home Assistant.

When you speak, the process will work like this:

```text
Echo Show microphone
        ↓
VACA
        ↓
Home Assistant voice pipeline
        ↓
Hermes speech-to-text
        ↓
Hermes conversation agent
        ↓
Hermes text-to-speech
        ↓
Echo Show speaker and display
```

## Step 6: Configure the Wake Word

Open the VACA app settings on the Echo Show.

Enable wake-word detection and select the wake word you want to use.

For this project, I will use:

```text
Hey Jarvis
```

Make sure microphone access and background operation are enabled.

VACA needs to keep running so it can listen for the wake word while the dashboard is displayed.

After enabling it, say:

```text
Hey Jarvis
```

Wait for the listening screen, and then say your command.

For example:

```text
Hey Jarvis, turn on my bedroom light.
```

The Echo Show should send the audio to Home Assistant, use the Hermes pipeline, and play the answer through its speaker.

## Step 8: Configure the Echo Show as a Dedicated Device

To make the Echo Show behave like a real smart display:

* Disable automatic sleep
* Keep the screen on while connected to power
* Allow VACA to run in the background
* Disable battery optimization for VACA
* Start VACA automatically after boot
* Enable full-screen or kiosk mode
* Hide the Android navigation bar if possible
* Keep the Echo Show connected to power

You can also configure the screen to turn off after a period of inactivity and wake up when someone approaches or activates the assistant.

## Result

The old Echo Show is now a self-hosted JARVIS smart display.

I can talk to JARVIS using a wake word without needing my phone or computer. The device can display information, control my smart home, play spoken responses, and show what JARVIS is doing.

This gives JARVIS both a voice and a face.
