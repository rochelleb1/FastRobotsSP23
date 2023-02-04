---
layout: default
---

# Lab 2: Bluetooth

This lab works to establish communication between the computer and the Artemis board through Bluetooth.

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

### Configurations
I work on Windows 11, so after attempting a lot of python and linux fixes, I used the fix posted by a fellow classmate to get bluetooth to work on WSL2 (Windows Subsystem for Linux). I first installed the "USB/IP Device", providing ownership of the Bluetooth USB to WSL2. I compiled a new kernel for WSL2, then setup the Bluetooth device. Commands that must be run after the Blutetooth device is newly plugged in are:

    usbipd wsl attach --busid=1-2
    sudo service dbus start
    sudo service bluetooth start

This allows for the **demo.ipynb** file to work and for connection to be allowed between the computer and the Artemis board.

### demo.ipynb
Using the fix above, I was able to connect to the Artemis board and run the initial cells as shown below:

<img src="/FastRobotsSP23/assets/images/democells.jpg" class="center" style="height: 400px;"/>

### Echo
The first task was to echo an input string with extra preceding characters 'Robot says ->' followed by the input string. Below is the code used to complete the task:

Arduino command code located within the switch case statement under case ECHO. The tx_estring_value will be written to the output in the **demo.ipynb** file:

    case ECHO:
        char char_arr[MAX_MSG_SIZE];
        
        success = robot_cmd.get_next_value(char_arr);
            if (!success)
                return;

        tx_estring_value.clear();
        tx_estring_value.append("Robot says: ");
        tx_estring_value.append(char_arr);
        tx_characteristic_string.writeValue(tx_estring_value.c_str());
    
        break;

Python code and output:

<img src="/FastRobotsSP23/assets/images/echo.jpg" class="center" style="height: 200px;"/>


### Get Time
This task required adding a command GET_TIME_MILLIS to make the robot reply with a string of the amount of time in milliseconds since the Artemis board began running the program. I added GET_TIME_MILLIS both to the switch-case statement in **ble_arduino.ino** as well as to **cmd_types.py**. I utilized the Arduino function **millis()** to get the time and sent back this value to be printed in **demo.ipynb**. Below is the Arduino and python code for the task:

Arduino command code:

    case GET_TIME_MILLIS:
        tx_estring_value.clear();
        tx_estring_value.append(millis());
        tx_characteristic_string.writeValue(tx_estring_value.c_str());

        break;

Python code and output:

<img src="/FastRobotsSP23/assets/images/time.jpg" class="center" style="height: 200px;"/>

### Notification Handler
Instead of receiving values one at a time, we can use a notification handler to constantly update and return a variable. We start by declaring a global variable to be accessed by the notification handler.

I defined a **callback_function** that takes arguments uuid, which is the ble.uuid of the type you are expecting to receive, i.e. *['RX_FLOAT']* in this case. Inside this function, we update the global variable to be the most update version, converting from bytearray to float, then printing the global variable.

We call the **callback_function** through **ble.start_notify**, which takes 2 arguments: the uuid of the expected type as well as the callback_function. Values will continue to be updated (incremented by 0.5) until **ble.stop_notify** is called, which takes an argument of the expected type uuid.

Below is the python code to process the task, and no Arduino code was added.
<img src="/FastRobotsSP23/assets/images/noti.jpg" class="center" style="height: 300px;"/>


### Get Temperature Command

### Limitations


<img src="/FastRobotsSP23/assets/images/construction.jpg" class="center" style="height: 400px;"/>

[Back to Homepage](../)
