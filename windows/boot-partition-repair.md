# Windows boot partition repair (GPT partitions)
It has happened to me numerous of times that I dualboot, but then decide to reinstall some distro on my linux drive, but oh no, windows has hijacked my linux boot partition. So when I wipe my linux drive, I cannot boot into windows anymore. This is a guide that aims to teach me/you how to resolve that once it inevitably happens.
## 0.1. What I exactly did to get myself in this situation for writing this guide
I installed windows 11 inside a VM on virtualbox (currently using windows, if I was on linux wouldve used qemu/kvm), then inserted a fedora iso into the vm and booted into that, then deleted the windows boot partition to emulate this scenario roughly.
<img width="510" height="379" alt="image" src="https://github.com/user-attachments/assets/6db70860-2941-4d7f-a728-f6f0fd88aab5" />
## 0.5. Backup your data from windows
If you're aware something like this is probably about to go down, please back up all the important data on your windows drive just in case. __Make sure to back up all important data, when doing this you're messing around with drives, one wrong command and the wrong partition is wiped__
## 1. Flash windows onto a usb stick
If you're on windows you use either the official [microsoft utility](https://www.microsoft.com/en-gb/software-download/windows11) *labeled Create Windows 11 Installation Media* or you can use my preffered method which is ofcourse [rufus](https://rufus.ie/en/). If you're on linux I would suggest you to just use ventoy for this since I have found balena etcher doesn't work. Whatever you do (*except the official way*) you need the windows iso which you can get [here](https://www.microsoft.com/en-gb/software-download/windows11)
## 2. Boot into your installation (recovery) media
Plug in your usb stick with a freshly flashed windows installation media into your computer, keep in mind we are not reinstalling windows so the procedure is not exactly the same. Hit the key you usually need to hit to boot into a usb drive, and select your usb stick.
## 3. Open terminal
Once you're in the installation media, you're not going to proceed to actually install windows, you're going to hit ```shift+f10``` and a cmd window is going to open.
<img width="987" height="513" alt="image" src="https://github.com/user-attachments/assets/07ae5278-8302-425c-b3c0-3b90e4570162" />

In the terminal you're going to type ```diskpart``` then you are going to list all the drives using ```list disk```
<img width="431" height="129" alt="image" src="https://github.com/user-attachments/assets/808c96bd-a9e3-4a12-a0b4-b2827239e21a" />

You are probably doing this on an actual computer so this is probably going to look a bit more complicated for you
Here you are choosing what drive you want your new boot partition to be on, *it is the smartest for this to be on the same drive as your main C: partition* you are going to type ```select disk <insert disk number>```
<img width="259" height="88" alt="image" src="https://github.com/user-attachments/assets/211e52aa-c92a-4589-bdab-666c5d88ef8a" />

Now we want to see all the partitions you have on the drive you're selected, we'll do that with ```list partitions```
<img width="419" height="124" alt="image" src="https://github.com/user-attachments/assets/f610d9b6-b549-4160-94ef-31871cfe5834" />
## Shrink drive (not needed if you have unallocated space for a new partition)
Now, if you have enough free(unallocated) space on the drive you have selected (500mb is more than enough), you can go on to the next step, if you do not have enough space you have to shrink some partitions.
To do that we'll use ```select partition <insert partition number>``` *(it is smartest to shrink a primary drive, so in this case the system drive)*
<img width="343" height="80" alt="image" src="https://github.com/user-attachments/assets/fe6096d8-875c-4c01-be1a-98b15f8d43fd" />

Then we'll use ```shrink desired=<amount you want to shrink>```
<img width="406" height="78" alt="image" src="https://github.com/user-attachments/assets/f4c8e4e1-30d9-408b-957b-35de9096e309" />
## Creating the new EFI boot partition
Then we have to ```select disk <the disk you're using for this>``` and then ```create partition efi size=<the size you want it to be (I recommend 512)>```. 
<img width="453" height="83" alt="image" src="https://github.com/user-attachments/assets/cc99a6aa-5673-46fb-8da7-dc2e51c95fc4" />

Now we select the newly created partition and format it with ```select partition <number of the new boot partition>``` (if you dont know what the number is run ```list partitions```) 
<img width="417" height="225" alt="image" src="https://github.com/user-attachments/assets/5a0509ea-5540-4d1e-b2df-752a332c7ff1" />
and then once selected ```format quick fs=fat32```
<img width="356" height="103" alt="image" src="https://github.com/user-attachments/assets/427e277c-f0ba-4c1e-ada3-b471e6169299" />










