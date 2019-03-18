# linux-max98090
ArchLinux repo with Linux kernel patched for better sound support for byt-max98090 devices on some Chromebooks. Starting with 4.20.1, packages will be configured for the Toshiba Chromebook2 (Swanky) running ext2/3/4, with support for USB sound, some crypto mods, and whatever else people deem worthy. 

* Added btrfs support 2-26-19. Removed 3-7-19, no longer needed. 
* Added bluetooth networking componenets 3-7-19 for hotspot tethering
* Added overlayfs for ram disk stuff 3-18-19

If you would like to include other modules going forward, please post an issue request. Reference the config file posted (thanks to DuffyDack for providing the intiial config) for the config used. 

## Readme

This is a continuation of the generous work of DuffyDack's ArchLinux repo. 

#### UCM & asound

It is recommended to load plbossart's UCM files first: 
* GitHub: https://github.com/plbossart/UCM
* AUR: https://aur.archlinux.org/packages/ucm_plbossart-git/

After this, install the kernel, reboot, remove the UCM files (via pacman if Arch based distro), and reboot again. Removing it should allow the volume to work properly and correct itself when opening pavucontrol with a live stream active. If you are missing the device after an update, try this reload / remove cycle again. 

Note, headphones don't seem to work without UCM (for me; others have not had this problem).
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
