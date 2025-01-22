![Diskpart](https://github.com/user-attachments/assets/c8a8d403-9e83-497c-a388-3ccea23df0a0)# Steps to Reset Password for Windows Server 2012

## Step 1: Create a Bootable Image of Windows Server 2012 Using Rufus
1. Download the ISO file for Windows Server 2012.
2. Download and install Rufus from [rufus.ie](https://rufus.ie).
3. Insert a USB drive with at least 8 GB of space.
4. Open Rufus and select the USB drive under "Device."
5. Click "SELECT" and browse to the ISO file for Windows Server 2012.
6. Under "Partition Scheme," choose "MBR" (for BIOS) or "GPT" (for UEFI) based on your server setup.
7. Click "START" and confirm the warning to create the bootable USB drive.
![Rufus](https://github.com/user-attachments/assets/e8e5eb6b-7ebc-480b-abc6-2a08b8e3601c)



## Step 2: Boot from USB and Access the Create Partition Wizard
1. Insert the USB drive into the server and restart it.
2. Enter the BIOS/UEFI on time boot (commonly by pressing `F11` for HP server during boot).
3. Wait for the boot menu to open and select the USB drive boot
4. Wait for ISO boot and the setup initialization.
5. Once the setup begins, select your language and click "Next."
6. Click "Install Now" to open the partition wizard.

## Step 3: Load the Correct RAID Driver
1. In the partition wizard, if no drives are visible, click on "Load Driver."
2. Insert the RAID driver disk or browse to the location of the RAID drivers.
3. Load the appropriate driver for your RAID controller, available on HP website.
4. After the driver is loaded, the logical drive should appear.

![Raid load](https://github.com/user-attachments/assets/ae929b92-877f-4c49-b277-c7313d0d32e6)


## Step 4: Open the Repair Menu and Access Command Prompt
1. Go back to the installation screen and click on "Repair your computer."
2. Select "Troubleshoot" from the available options.
3. Choose "Command Prompt."
![Repair](https://github.com/user-attachments/assets/53a74703-421b-4aa6-bab8-840a8daf0499)

## Step 5: Check Volume Using Diskpart
1. In Command Prompt, type `diskpart` and press `Enter`.
2. Type `list volume` to display all available volumes.
3. Locate the volume containing the `Windows` folder (in my example Volume H).
![Diskpart](https://github.com/user-attachments/assets/c9850d7e-2d64-4aaa-af50-5f124c78ed18)


## Step 6: Rename `utilman.exe` and `cmd.exe`
1. Change to the Windows folder by typing:  
   `cd C:\Windows\System32` (replace `C:` with the drive letter where Windows is installed).
2. Rename `utilman.exe` as a backup:  
   `rename utilman.exe utilman-bkup.exe`
3. Rename `cmd.exe` as `utilman.exe`:  
   `rename cmd.exe utilman.exe`

## Step 7: Boot Normally to Windows Server
1. Close Command Prompt and restart the server.
2. Boot from the logical drive containing Windows Server.

## Step 8: Access Command Prompt via Ease of Access
1. On the login screen, click the "Ease of Access" button in the bottom-right corner.
2. A Command Prompt window will appear.
   ![Windows-Live-Writer-Resetting-the-Domain-Administrator-passw_3166-image_4](https://github.com/user-attachments/assets/c45d31e1-6f33-4f1c-add7-8d75cf775aff)


## Step 9: Reset the Password
1. In the Command Prompt, use the `net user` command to reset the password:  
   `net user <username> <newpassword>`  
   Replace `<username>` with the account name and `<newpassword>` with the desired password.
2. Close the Command Prompt and log in with the new password.

