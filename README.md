# monkey_std_msgs

**monkey_std_msgs** is a ROS2 package that provides standard custom messages, including actions and services, used by Monkey Robotics. This package is designed to be easily extendable, so you can add new custom messages that may be useful in other projects.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Authors](#authors)

---

## Overview

This package is part of the Monkey Robotics ecosystem, facilitating seamless communication through custom ROS2 message types. It supports automatic detection and registration of new message types added to the `/action` and `/srv` directories.

## Features
- **Automatic Registration**: The package is designed to detect and register messages dynamically—no manual changes needed in the `CMakeLists.txt` file.

---

## Installation

To use `monkey_std_msgs`, ensure you have ROS2 installed and follow these steps:

Clone the repository into your ROS2 workspace:
   ```bash
   https://github.com/MonKey-Robotics/monkey_std_msgs.git
   ```

## Usage
Example use case:
```
monkey_std_msgs/
├── action/
│   └── MyCustomAction.action
├── srv/
│   └── MyCustomService.srv
├── msg/
│   └── MyCustomAction.msg
└── package.xml
```

You may add your own custom .action, .srv, or .msg files in the directory shown in this example. There is no need to maunally update the `CMakeLists.txt` file as it can find the files automatically.
   

## Authors
[@KaiYuanBu](https://github.com/KaiYuanBu)
