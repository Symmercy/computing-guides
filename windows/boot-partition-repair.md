# Windows boot partition repair
It has happened to me numerous of times that I dualboot, but then decide to reinstall some distro on my linux drive, but oh no, windows has hijacked my linux boot partition. So when I wipe my linux drive, I cannot boot into windows anymore. This is a guide that aims to teach me/you how to resolve that once it inevitably happens.
## 0.1. What I exactly did to get myself in this situation for writing this guide
I installed windows 11 inside a VM on virtualbox (currently using windows, if I was on linux wouldve used qemu/kvm), then inserted a fedora iso into the vm and booted into that, then deleted the windows boot partition to emulate this scenario roughly.
<img width="510" height="379" alt="image" src="https://github.com/user-attachments/assets/6db70860-2941-4d7f-a728-f6f0fd88aab5" />

## 0.5. Backup your data from windows
If you're aware something like this is probably about to go down, please back up all the important data on your windows drive just in case.
## 1. Flash windows onto a usb stick
If you're on windows you use either the official [microsoft utility](https://www.microsoft.com/en-gb/software-download/windows11) *labeled Create Windows 11 Installation Media* or you can use my preffered method which is ofcourse [rufus](https://rufus.ie/en/). If you're on linux I would suggest you to just use ventoy for this since I have found balena etcher doesn't work. Whatever you do (*except the official way*) you need the windows iso which you can get [here](https://www.microsoft.com/en-gb/software-download/windows11)
## 2. Boot into your installation (recovery) media
Plug in your usb stick with a freshly flashed windows installation media into your computer, keep in mind we are not reinstalling windows so the procedure is not exactly the same. Hit the key you usually need to hit to boot into a usb drive, and select your usb stick.
## 3. Open terminal, do the operation.
Once you're in the installation media, you're not going to proceed to actually install windows, you're going to hit ```shift+f10``` and a cmd window is going to open.
In the terminal you're going to type ```diskpart``` then you are going to list all the drives using ```list disk```
