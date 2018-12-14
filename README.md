# linux-max98090
ArchLinux repo with Linux kernel patched for better sound support for byt-max98090 devices on some Chromebooks

#Readme

This is a continuation of the generous work of DuffyDack's ArchLinux repo. 

I try to test this and keep as up to date as possible, but have limited time, please use at ***your own risk***, test, and submit any issues. 

- Add the repo to your /etc/pacman.conf

	[jskier]
	Server = https://github.com/JSkier21/linux-max98090/releases/download/latest

- Add and sign my key

	sudo pacman-key --recv-keys 9B93DC9F02622EC55E008F27D06F79ACB2473D56
	sudo pacman-key --lsign-key 9B93DC9F02622EC55E008F27D06F79ACB2473D56

- Install kernel (headers are optional)

	sudo pacman -Syu linux-max98090 linux-max98090-headers

- Bootloader will need to be configured, and should reference this custom kernel files, linux-max98090. Refence https://wiki.archlinux.org/index.php/Arch_boot_process#Boot_loader

#Details

The latest issue with sound is a regression introduced in 4.18.15, commit [2], broke sound. 

[1] https://patchwork.kernel.org/patch/10667953/

[2] https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/?id=9f8318a1c50c77f20909b0f615ee4113d935e660
