# Shadow Dexterous Hand Software Installation

Last reviewed: `September 2024`

## Introduction

This document serves as an introductory guide to help new collaborators on projects that use the Shadow Robotic Hand.

It will go through the steps of installing the container provided by the manufacturer on personal computers and make the necessary changes to it in order to make it operational with BioIK kinematics solver.

### Requirements

This installation was tested on Ubuntu 20.04 and 22.04 systems so it is recommend that you use one of this versions of OS.

Additionally, before proceeding, ensure that your graphics card drivers are installed.

Lastly, to install curl, you can use the following command:
```bash
  sudo snap install curl
```

## Running the one-liner

Before running the command provided by Shadow that installs docker and the server container **your computer must be physically connected to the NUC** that executes the control loop of the hand.

Please ask for access to this device if you intend to perform the installation process.

Before running the one-liner, check how is the usb to ethernet adapter being recognized by your system, for this run `ifconfig`.

  If the device interface name starts with `enx`, run the following command (original Shadow one-liner):
  ```bash
    bash <(curl -Ls https://raw.githubusercontent.com/shadow-robot/aurora/v2.2.5.1/bin/run-ansible.sh) server_and_nuc_deploy --branch v2.2.5.1 --read-secure customer_key product=hand_e tag=noetic-v1.0.31 reinstall=true
  ```

  Else if the device interface name starts with `eth`, run the following command:
  ```bash
    bash <(curl -Ls https://raw.githubusercontent.com/DIGI2-FEUP/aurora-2.2.5.1/master/bin/run-ansible.sh) server_and_nuc_deploy --read-secure customer_key product=hand_e tag=noetic-v1.0.31 reinstall=true
  ```
📝 Note: If the installation process ends with an error, try running the command again. If the error persist, restart the pc and then try running the installation command again. After some tries, if the error still persists, please contact Shadow support at: `support@shadowrobot.com`.

During the installation process you will be prompted to insert some credentials. These are printed in a laminated sheet that is kept in the case of the Shadow Hand.

This should create a few icons on your desktop. You can use the “Shadow Launcher" to access utilities of the software package. 

Inside it you will find a folder called “Shadow Advanced Launchers" containing “1 - Launch Server Container". This will launch the docker container on your computer that you can use to run your code and interact with the hand or simulation.

## Troubleshooting Installation Errors

If you encounter an error during the installation process, it might be caused by outdated installation components. In such cases, it is recommended to check for newer versions of the files referenced in the error message.

To do this, navigate to the original [repository](https://github.com/shadow-robot/aurora) on GitHub:

Locate the specific file mentioned in the error message and check for any recent updates or changes.

It is possible that the issue has been addressed in a more recent version of the file.

## BioIK Kinematic Solver Instalation

Inside the docker container run:

  ```bash
    sudo apt-get update
  ```

  ```bash
    sudo apt-get install libglfw3 libglfw3-dev
  ```

  ```bash
    cd ~/projects/shadow_robot/base/src/
  ```

  ```bash
    sudo rm -r sr_interface
  ```

  ```bash
    git clone https://github.com/DIGI2-FEUP/Shadow-v2.2.5.1-Software-Install.git
  ```

  ```bash
    sudo mv Shadow-v2.2.5.1-Software-Install/sr_interface .
  ```

  ```bash
    sudo rm -r Shadow-v2.2.5.1-Software-Install
  ```

  ```bash
    git clone https://github.com/TAMS-Group/bio_ik.git
  ```

  ```bash
    cd ..
  ```

  ```bash
    catkin_make
  ```

  ```bash
    echo "source /home/user/projects/shadow_robot/base/devel/setup.bash" >> /home/user/.bashrc
  ```

Restart the server container.

## Conclusion

If you run into any issues please do not hesitate in contacting me via e-mail or Slack, whichever is most convenient to you.

Best of luck in your developments!


Francisco Ribeiro (fmribeiro@fe.up.pt)

Bruno Santos (brunosantos@fe.up.pt)

DIGI2
