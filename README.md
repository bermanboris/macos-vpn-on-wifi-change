# Auto Connect to VPN on Specific Wi-Fi for macOS

This script is designed for macOS users who want to automate connecting to a specific VPN when their computer connects to a designated Wi-Fi network. It's efficient, requires no additional configuration files or binaries, and does not need administrative privileges to run.

## Features

- 📁 No external configuration files or binaries needed.
- 🔄 Automatically loads upon user login.
- 🔒 No root or admin access required.
- ✅ Highly efficient and lightweight.

Tested and confirmed working on macOS Sonoma (14.1).

## Prerequisites

Before you begin, ensure you have the following:
- Basic knowledge of terminal operations in macOS.
- Access to your macOS user account's Library folder.

## Installation

1. **Download the Launch Agent File:**
   Navigate to the directory where you want to place the Launch Agent, and run the following command:

   ```shell
   curl -L https://github.com/bermanboris/macos-vpn-on-wifi-change/raw/main/com.user.networkwatcher.plist -o ~/Library/LaunchAgents/com.user.networkwatcher.plist
   ```

2. **Customize the Launch Agent:**
   Set your specific Wi-Fi network and VPN service names by first defining them as variables. Replace `<Your WiFi Name>` and `<Your VPN Name>` with your actual Wi-Fi and VPN names:

   ```shell
   WIFI_NAME="<Your WiFi Name>"
   VPN_NAME="<Your VPN Name>"
   ```

   Next, use these variables to update your .plist file:
   ```shell
   sed -i '' "s/<Your WiFi Name>/$WIFI_NAME/g" ~/Library/LaunchAgents/com.user.networkwatcher.plist
   sed -i '' "s/<Your VPN Name>/$VPN_NAME/g" ~/Library/LaunchAgents/com.user.networkwatcher.plist
   ```


3. **Load the Launch Agent:**
    To activate the Launch Agent without needing to reboot or log out, run the following command in the Terminal:
   ```shell
   launchctl load ~/Library/LaunchAgents/com.user.networkwatcher.plist
   ```



## Uninstallation

If you need to remove the Launch Agent and stop it from managing your VPN connections, follow these steps:

1. **Unload the Launch Agent:**
   Before deleting the Launch Agent file, ensure it's unloaded from your system to prevent it from being automatically reloaded by the system. Run the following command in the Terminal:

   ```shell
   launchctl unload ~/Library/LaunchAgents/com.user.networkwatcher.plist


2. **Remove the Launch Agent File:**
   After unloading the Launch Agent, you can safely delete the .plist file. Use the following command to remove it:

   ```shell
   rm ~/Library/LaunchAgents/com.user.networkwatcher.plist
   ```

## How It Works

Once installed, the script will monitor your Mac's network connection (by watching network related files changes). When it detects a connection to the specified Wi-Fi network, it will automatically attempt to connect to the specified VPN. If the network connection changes away from the specified Wi-Fi network, it will disconnect from the VPN.

## Troubleshooting

If you encounter issues with the script not functioning as expected, ensure the SSID and VPN names are correctly entered. Also, check that the .plist file has correct syntax and is located in the proper directory.


## Contributions

Contributions are welcome! If you'd like to improve the script or add features, please fork the repository and submit a pull request.
