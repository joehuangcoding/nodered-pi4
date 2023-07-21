# nodered-pi4
# node-red and run as service
To install Node-RED with the built-in MQTT server on a Raspberry Pi 4, you can follow these steps:

1. Start by updating your Raspberry Pi's package repositories by opening a terminal or SSH session and running the following commands:

```shell
sudo apt update
sudo apt upgrade
```

2. Install Node.js and npm (Node Package Manager) by running the following command:

```shell
sudo apt install nodejs npm
```

3. Install Node-RED globally using npm:

```shell
sudo npm install -g --unsafe-perm node-red
```

4. Verify the installation by running `node-red` in the terminal. You should see output indicating that Node-RED is running and listening on a port (usually 1880).

5. To automatically start Node-RED on boot, you can use `systemd`. Create a service file for Node-RED by running the following command:

```shell
sudo nano /etc/systemd/system/nodered.service
```

6. In the nano text editor, paste the following service configuration:

```plaintext
[Unit]
Description=Node-RED
After=syslog.target network.target

[Service]
ExecStart=/usr/bin/env node-red-pi --max-old-space-size=256 -v
Restart=on-failure
User=pi
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```

7. Save and exit the nano editor by pressing `Ctrl+X`, `Y`, and `Enter`.

8. Enable and start the Node-RED service using the following commands:

```shell
sudo systemctl enable nodered.service
sudo systemctl start nodered.service
```

9. Now, open your web browser and access the Node-RED editor by navigating to `http://<raspberry-pi-ip-address>:1880`.

10. In the Node-RED editor, click on the hamburger menu (top right corner) and select "Manage palette."

11. In the "Manage palette" menu, go to the "Install" tab and search for "node-red-contrib-mqtt-broker". Install the "node-red-contrib-mqtt-broker" package, which provides the built-in MQTT broker node.

12. Once the package is installed, close the "Manage palette" menu and drag the "mqtt" node from the "network" category onto the Node-RED workspace.

13. Double-click on the "mqtt" node to configure its properties, such as the listening port and other settings. By default, it listens on port 1883.

14. Click "Done" to save the configuration.

15. Deploy the changes by clicking the "Deploy" button in the top-right corner of the Node-RED editor.

Now, you have Node-RED installed on your Raspberry Pi 4 with the built-in MQTT server. You can use the MQTT nodes in Node-RED to publish and subscribe to MQTT topics, and you can connect to the built-in MQTT broker using MQTT client applications or other devices in your network.

# Install nodejs 14 and enable authentication
To install Node-RED and set up a password on a Raspberry Pi 4, you can follow these steps:

1. Install Node.js: Open a terminal or SSH into your Raspberry Pi and run the following commands to install Node.js:

   ```bash
   curl -sL https://deb.nodesource.com/setup_14.x | sudo bash -
   sudo apt-get install -y nodejs
   ```

2. Install Node-RED: Run the following command to install Node-RED globally:

   ```bash
   sudo npm install -g --unsafe-perm node-red
   ```

3. Start Node-RED: Launch Node-RED by running the following command:

   ```bash
   node-red
   ```

   Node-RED will start running, and you can access the editor by navigating to `http://localhost:1880` in a web browser on your Raspberry Pi.

4. Set up a password: Stop the Node-RED server by pressing `Ctrl+C` in the terminal where it's running.

5. Generate hashed password: Run the following command to generate a hashed password for authentication:

   ```bash
   node-red-admin hash-pw
   ```

   Enter a password when prompted, and make note of the hashed password that is generated.

6. Configure the settings file: Open the settings.js file located at `~/.node-red/settings.js` (or `%userprofile%/.node-red/settings.js` on Windows) using a text editor.

7. Uncomment and modify the adminAuth section: Locate the `adminAuth` section in the settings.js file and modify it as follows:

   ```javascript
   adminAuth: {
       type: "credentials",
       users: [{
           username: "admin",
           password: "<hashed_password>",
           permissions: "*"
       }]
   },
   ```

   Replace `<hashed_password>` with the hashed password you generated in step 5.

8. Save the file and start Node-RED: Save the changes to the settings.js file, and start Node-RED again by running the command:

   ```bash
   node-red
   ```

   Node-RED will now require a password for authentication.

9. Access Node-RED with password: Open a web browser on your Raspberry Pi or another device connected to the same network, and navigate to `http://<raspberry_pi_ip_address>:1880`. You will be prompted to enter a username and password. Use "admin" as the username and enter the password you set in step 5.

That's it! You have successfully installed Node-RED on your Raspberry Pi 4 and set up a password for authentication. Now, only authenticated users can access the Node-RED editor.

# Commands for service
To manage the Node-RED service on a Raspberry Pi, you can use the `systemctl` command, which is the standard command for controlling services in systemd-based Linux distributions. Here are the commands for starting, stopping, and checking the status of the Node-RED service:

1. Start Node-RED service:
```
sudo systemctl start nodered
```

2. Stop Node-RED service:
```
sudo systemctl stop nodered
```

3. Restart Node-RED service:
```
sudo systemctl restart nodered
```

4. Check the status of Node-RED service:
```
sudo systemctl status nodered
```

# This command will display a list of nearby BLE devices along with their MAC addresses. Make note of the MAC address of the specific BLE device you want to connect to.

Pair and connect to the desired BLE device. Use the bluetoothctl utility to interact with Bluetooth devices. Start the utility by entering the following command:

Copy code
bluetoothctl
Once you're inside the bluetoothctl prompt, you can use the following commands to pair and connect to the BLE device:

Enter power on to turn on the Bluetooth adapter (if not already on).
Enter scan on to start scanning for BLE devices.
Locate the MAC address of your desired BLE device from the scan results.
Enter pair <MAC_ADDRESS> to initiate the pairing process. Replace <MAC_ADDRESS> with the actual MAC address of the BLE device.
Follow any additional instructions prompted by the pairing process.
Enter connect <MAC_ADDRESS> to establish a connection to the BLE device.
Once the connection is established, you can interact with the BLE device by reading from or writing to its characteristics using tools like gatttool or programming languages like Python with libraries such as pygatt or bluepy.

These steps should help you connect your Raspberry Pi 4 to a Bluetooth Low Energy (BLE) device. Remember to adapt the instructions to your specific use case and the tools and libraries you prefer to work with.

