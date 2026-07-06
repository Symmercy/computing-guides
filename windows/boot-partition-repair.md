# Windows boot partition repair
It has happened to me numerous of times that I dualboot, but then decide to reinstall some distro on my linux drive, but oh no, windows has hijacked my linux boot partition. So when I wipe my linux drive, I cannot boot into windows anymore. This is a guide that aims to teach me/you how to resolve that once it inevitably happens.
## 1. Flash windows onto a usb stick
If you're on windows you use either the official [microsoft utility](https://www.microsoft.com/en-gb/software-download/windows11) *labeled Create Windows 11 Installation Media* or you can use my preffered method which is ofcourse [rufus](https://rufus.ie/en/). If you're on linux I would suggest you to just use ventoy for this since I have found balena etcher doesn't work.
## 2. Boot into your installation (recovery) media
Plug in your usb stick with a freshly flashed windows installation media into your computer, keep in mind we are not reinstalling windows so the procedure is not exactly the same
