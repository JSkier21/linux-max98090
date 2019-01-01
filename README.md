# linux-max98090
ArchLinux repo with Linux kernel patched for better sound support for byt-max98090 devices on some Chromebooks

## Readme

This is a continuation of the generous work of DuffyDack's ArchLinux repo. 

#### UCM & asound

It is recommended to load plbossart's UCM files first: 
* GitHub: https://github.com/plbossart/UCM
* AUR: https://aur.archlinux.org/packages/ucm_plbossart-git/

After this, install the kernel, reboot, remove the UCM files (via pacman if Arch based distro), and reboot again. Removing it should allow the volume to work properly and correct itself when opening pavucontrol with a live stream active. If you are missing the device after an update, try this reload / remove cycle again. 

Note, headphones don't seem to work without them. Your mileage may vary. Higher volume and more reliability are worth no headphones from the internal port to me (using a USB audio dongle works great for this if needed). UPDATE: DuffyDack is reporting that headphones work for him with asound config. I apparently did not migrate this file after a reinstall. I have not tested this yet myself (he's probably correct), however am including his asound.conf file for use in the repo. 

***

I try to test this and keep as up to date as possible, but have limited time, please use at ***your own risk***, test, and submit any issues. These files are often based on Arch Core, but sometimes Testing or Staging may be used (mainilne kernel). Should in theory work on other ArchLinux based distros. In any case, keep another known working kernel image installed and available to boot. 

Add the repo to your /etc/pacman.conf

	[jskier]
	Server = https://github.com/JSkier21/linux-max98090/releases/download/latest

Add and sign my key

	sudo pacman-key --recv-keys 9B93DC9F02622EC55E008F27D06F79ACB2473D56
	sudo pacman-key --lsign-key 9B93DC9F02622EC55E008F27D06F79ACB2473D56

 Install kernel (headers are optional)

	sudo pacman -Syu linux-max98090 linux-max98090-headers

Bootloader will need to be configured, and should reference the custom kernel files, linux-max98090. Refence https://wiki.archlinux.org/index.php/Arch_boot_process#Boot_loader

## Details

The latest issue with sound is a regression introduced in 4.18.15, commit [2], broke sound. 

[1] https://patchwork.kernel.org/patch/10667953/

[2] https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/?id=9f8318a1c50c77f20909b0f615ee4113d935e660
