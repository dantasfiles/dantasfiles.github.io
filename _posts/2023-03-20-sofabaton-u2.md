---
title: SofaBaton U2 universal remote setup
description: My Logitech Harmony remote finally broke, and I replaced it with a Sofabaton U2 remote. Here's how I made the change.
author: Daniel Dantas
---

My Logitech Harmony remote finally broke, and I replaced it with a Sofabaton U2 remote. Here's how I made the change.
  
## My setup

I have two boxes, a Verizon FIOS DVR for TV channels, and a [Roku Ultra](https://www.roku.com/products/roku-ultra) for streaming services.

Both the Verizon and Roku boxes are connected to an Panasonic television by HDMI cables. 

The television is connected to a Yamaha receiver (and thus to the [5.1 speaker system](https://en.wikipedia.org/wiki/5.1_surround_sound)) with an [optical audio cable](https://en.wikipedia.org/wiki/TOSLINK).

My [ **DVR** & **Roku** → _hdmi_ → **TV** → _optical_ → **Receiver**] is not the traditional connection, usually the recommended connection is [ **DVR** & **Roku** → _hdmi_ → **Receiver** → _hdmi_ → **TV**].   
However, my receiver is old and doesn’t support, or pass-through, modern HDMI features, so it was best to hook the boxes directly to the television instead.

## Setting up the DVR activity

The remote’s setup app instructs you to set up devices, not activities, but ignoring the instructions and setting up activities manually made more sense for me.

I first set up a DVR activity.

First, install and open the SofaBaton app. Click **U Series** :

![image](https://github.com/user-attachments/assets/637bb4d9-70bc-435a-b4e4-15a4d1f5f1af)

Follow the pairing instructions:

![image](https://github.com/user-attachments/assets/37028204-3b51-4477-9684-fa9a9a0688d3)

Click **Add** :

![image](https://github.com/user-attachments/assets/c95aadac-7058-486d-a802-5cb989e9e053)

Choose **Infrared (IR)** :

![image](https://github.com/user-attachments/assets/f42b5699-edff-4994-8c99-fea413cfac94)

You can search for your device in the SofaBaton database. However, sometimes the database for a device is a bit off, and sometimes it’s hard to determine which text description in the database maps to which physical button on the original remote. 

So I ended up choosing **Learn from original IR** remote and learning the buttons manually from the original remotes. It took little more time than deciphering the database did, and this way I knew all the button mappings were what I explicitly wanted.

![image](https://github.com/user-attachments/assets/cf6a53f8-385f-477c-8bdb-f7868f5fd353)

Click **Next** :

![image](https://github.com/user-attachments/assets/3e85f8f7-56a5-4969-be0e-a31d86a83b54)

You’ll now be on the main learning screen:

![image](https://github.com/user-attachments/assets/b9f64d67-3348-46de-b93f-5b0aacf63bb3)

  * The **⏻TV** button on the SofaBaton remote is learned from the power button on the original television remote.

  * The **⭲** button on the top right of the SofaBaton remote is learned from the “ _switch to the DVR HDMI input on the television_ ” button from the original television remote. This button is crucial, as it is used to switch from the Roku to the DVR.

  * The volume buttons (🔊🔉🔇) on the SofaBaton remote are learned from the volume buttons on the original receiver remote.

  * All remaining buttons on the SofaBaton remote are learned from the original DVR remote.

The result of all this learning from the television remote, the receiver remote, and the DVR remote is essentially a **DVR** activity:

![image](https://github.com/user-attachments/assets/9fc8ee05-a8f3-46fc-9a83-b324c42dcbf2)

To switch from the Roku to the DVR, I press the **⭲** button on the top right of the SofaBaton remote, which switches the HDMI input on the television to the DVR. 

## Setting up the Roku

I initially set up the Sofabaton to control the Roku, but eventually deleted that activity. My Roku has an advanced [Voice Remote Pro (2nd edition)](https://www.roku.com/products/accessories/roku-voice-remote-pro-2nd-edition), which can take voice commands, and uses a Wifi connection, so you don’t have to aim the remote like you do with infrared remotes. As such, the Roku remote is far superior in controlling the Roku than a universal remote.

In addition, with my television, pushing any button on the Roku remote turns on the television if it’s off, and switches the television to the correct HDMI input. So most of the framework of a **Roku** activity is already in place without a universal remote.

The only thing that the Roku remote can’t control is the receiver’s volume. Roku remotes can control television volume, but not receiver volume.

For controlling the volume, and the volume alone, I use the Sofabaton remote. There’s no need to switch the SofaBaton remote from its original **DVR** activity since that activity also correctly controls the receiver’s volume.

## Final Settings

To make the batteries last as long as possible, I make the SofaBaton remote screen as dim as possible since I never switch it from the **DVR** activity.

Click the menu in the top left, then the **Settings** :

![image](https://github.com/user-attachments/assets/e7437b0e-99ff-4077-83a2-3f4d90b90271)

The following are the settings I use to make the SofaBaton remote screen as dim as possible and preserve battery life:

![image](https://github.com/user-attachments/assets/dededf74-dd2f-4228-a4bf-4dee120319a6)
