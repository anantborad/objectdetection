# EAST Object Detection for Android/Edge Devices

This library is a simple object detection program made to recognize simple household objects and human faces.
## Installation

### Step 1: Install/Open Bash

#### Windows
Open [Windows Powershell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.3) (available on Windows 7 and later) on your computer.

#### Mac OS
1. Open the terminal application
2. List available shells by typing ```cat /etc/shells```.
Note down the path to bash such as ```/bin/bash```.
3. To update your account to use bash run ```chsh -s /bin/bash```.

### Step 2: Install [Git](https://git-scm.com/downloads)
If you opened Powershell, skip this step. 

If you are on mac, follow the next steps: 
1. Check if you have git installed by typing ``git``. 
2. If is says ``usage: ...`` and continues on, skip to the next big step.
3. If it does not say ``usage: ...`` and other data and instead throws an error with red text, click on the above link.
4. Download the correct version of git for your operating system and execute the file once it is completed. A walkthrough window will then pop up.
4. Click on 'next' for all of the slides and press 'install'. Git will then take less than 2 minutes to install on your computer.
5. Once it is done, type ``git`` on the terminal. If it still throws an error, close and reopen the terminal. If the problem persists, contact me at [my email](mailto:anant.borad@academicsplus.org).

### Step 3: Install the Library
1. First, decide where you want to keep the library. Run ``cd ~/Desktop~``.
2. This will create a new folder in your desktop in future steps. If you want to nest the library in a folder (which you can then look at in the file explorer), run ``mkdir nameofthefolder`` and then ``cd nameofthefolder``.
3. Copy/Paste and Execute the following line in the terminal:
```bash
git clone https://github.com/anantborad/objectdetection.git objectdetector
```
Then run ``cd objectdetector``.


## Step 2: Install Requirements
You should now be in the library folder on your terminal. In the library, I have created a shell script that will install everything for you. 

In order to run it, however, you first have to install the [Chocolatey Software](https://chocolatey.org/install). Open the website and follow all of the instructions on it to install it onto your computer. The website should have instructions for different operating systems. If not, [email me](mailto:anant.borad@academicsplus.org).

Run the following line:
```zsh
bash ./get_pi_requirements.sh
```
Congratulations, you've successfully installed the library!
# Usage

## License

[MIT](https://choosealicense.com/licenses/mit/)
