# Raspberry Pi with DAKboard calendar wall display
Setting up a Raspberry Pi with DAKboard for a wall display involves several steps, including installing the operating system, configuring the Pi, and setting up DAKboard. Here's a step-by-step guide to help you through the process:

### Components Needed:
1. **Raspberry Pi** (any model that supports display output)
2. **Monitor or Display** (IPS Monitor With Vesa mount)
3. **MicroSD Card** (with Raspberry Pi OS installed)
4. **Power Supply** for the Raspberry Pi
5. **DAKboard Account** (free or paid, depending on features you need)
6. **Case and Frame** (optional, to enclose the display and Pi for wall mounting)
7. **Keyboard and Mouse** (for initial setup)
8. **WiFi or Ethernet** (for internet access)
9. **TV Wall Mount** (mount the monitor the wall using VESA)

### Steps to Set Up:

#### 1. **Prepare the Raspberry Pi:**
   - **Install Raspberry Pi OS** on the MicroSD card using [Raspberry Pi Imager](https://www.raspberrypi.com/software/) or [Balena Etcher](https://etcher.balena.io/).
   - Boot up the Raspberry Pi with a connected keyboard, mouse, and display.
   - **Set up WiFi** and perform any necessary updates.

#### 2. **Create a DAKboard Account:**
   - If you haven’t already done so, create an [account](https://dakboard.com/pricing) (free!) and configure DAKboard.
   - In DAKboard, you can customize your display with a **calendar**, **to-do lists**, **weather**, **news feeds**, and even **photos**.
   - Link your calendar service (Google Calendar, iCloud, Outlook, etc.) for seamless updates.


#### 3: Configure the Raspberry Pi for Auto-Launch of DAKboard:
You want the Raspberry Pi to automatically launch Chromium in full-screen mode and open DAKboard’s custom URL.

1. **Open Terminal:**
   - Open the Terminal on your Raspberry Pi.

2. **Install Chromium Browser:**
   - Update your system: `sudo apt update && sudo apt upgrade -y`
   - Install Chromium: `sudo apt install -y chromium-browser unclutter`
   - Install Unclutter: `sudo apt install -y unclutter`


3. **Set Up Chromium to Launch DAKboard on Boot:**
   - Create the directory `mkdir -p ~/.config/lxsession/LXDE-pi`
   - Open the autostart file: `nano ~/.config/lxsession/LXDE-pi/autostart`
   - Add the following line at the end of the file to launch Chromium in full-screen mode pointing to DAKboard. see example configuration [~/.config/lxsession/LXDE-pi/autostart](.config/lxsession/LXDE-pi/autostart)

4. **Save and Exit:**
   - Press `CTRL + X`, then `Y`, and `Enter` to save and exit the file.

### 4: Configure Display Settings
1. **Disable Screen Blanking:**
   - Open the lightdm.conf file: `sudo nano /etc/lightdm/lightdm.conf`
   - Find and uncomment the following lines by removing the `#`:
     ```
     [SeatDefaults]
     xserver-command=X -s 0 -dpms
     ```

    see example configuration [/etc/lightdm/lightdm.conf](etc/lightdm/lightdm.conf)

Add one of the following lines depending on the desired orientation:

  - For 90° clockwise rotation: `display_rotate=1`
  - For 180° rotation: `display_rotate=2`
  - For 270° clockwise rotation: `display_rotate=3`

2. **Save and Exit:**
   - Press `CTRL + X`, then `Y`, and `Enter` to save and exit the file.


#### 5. **Set Up Chromium to Launch DAKboard on Boot:**
Additional Configuration:
Use a framebuffer depth of 24 bits for better color.
   - Open the autostart file: `sudo nano /boot/config.txt`
   - Add the following line to the file.


	# Use 24 bit colors
	framebuffer_depth=24

see example: [/boot/config.txt](boot/config.txt)

#### 6. **Reboot and Test:**
   - Reboot the Raspberry Pi with:
     ```bash
     sudo reboot
     ```
   - After rebooting, the Pi should automatically launch the DAKboard calendar display in full-screen mode.

#### 7. Mount the Display:

You can now mount the monitor or display screen on your wall.
Use a VESA wall mount or a frame that hides the Pi behind the screen for a clean look.

Your Raspberry Pi should now be set up as a wall display with DAKboard. Enjoy your new digital display!