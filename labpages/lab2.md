---
layout: default
---

# Lab 2: Bluetooth

## Prelab

### Setup
The first setup steps were to update versions of Python 3 and pip. I then installed virtual environment (venv) and created a new virtual environment 'FastRobots_ble', which will be a folder within the general Lab folder along with ble_robot-1.1. Before any work can be done in this lab, the virtual environment must be activated using command `.\FastRobots_ble\Scripts\activate`. After installing the required python packages, I uploaded **ble_arduino.ino** to the Artemis board to receive the MAC address `c0:7:94:96:ab:44`.

### Codebase
We will use logging to display output messages during debugging, which prints messages to the standard output in addition to **ble.log**.
Some functions used to send and receive data to/from the Artemis board are:
* **reload_config()** to reload changes
* **connect()** to connect to Artemis board using MAC address above
* **disconnect()**
* **is_connection()** to indicate whether the controller is connected to the Artemis board
* **send_command(cmd_type,data)** to send a command with its data to the board
* **receive_xxx()** to read the GATT characteristic of the indicated type in place of **xxx**
* **start_notify(uuid, notification_handler)** to begin notifications on the characteristic specified by its uuid
* **bytearray_to_xxx** to convert the bytearray to type **xxx**
* **stop_notify(uuid)** to stop notifications on the specific characteristic specified by uuid

In the Arduino file, we have BLE UUIDs, Universally Uniquie Identifiers to distinguish the data sent between the board and the computer. The **BLExxxCharacteristc** constructors allow the data provided by Arduino BLE to be manipulated and used by the user using **BLERead, BLEWrite, BLENotify**. Lastly, we have the **RobotCommand** to be used when receiving and altering values of the form of a robot command `<cmd_type>:<val1>|<val2>|...`.

## Lab Tasks

<img src="/FastRobotsSP23/assets/images/construction.jpg" class="center" style="height: 400px;"/>

[Back to Homepage](../)
