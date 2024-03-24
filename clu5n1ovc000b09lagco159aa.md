---
title: "NixOS: OS as Code"
datePublished: Sun Mar 24 2024 14:52:37 GMT+0000 (Coordinated Universal Time)
cuid: clu5n1ovc000b09lagco159aa
slug: nixos
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711290328715/4c1649c8-9201-4b40-9b43-ce64cddc2dde.png

---

There are many Linux-based distributions out there, some are flashy, some are minimal, some are bloated (i guess we all hate those ones, lol). Then we have NixOS, a very fundamentally different Linux distro from all its other relatives. It can be summarized in three words: declarative, reproducible, and immutable.

## Declarative

Let's start with the first attribute, NixOS's declarative configuration makes it easy to write configurations for the various components in our operating system in an easy-to-understand language called "Nix". Nix is very similar to JSON syntax wise.  
For declaring NixOS config, we write a file called `configuration.nix` which is stored in `/etc/nixos/`

```nix
{
  imports =
    [ # Include the results of the hardware scan.
      ./hardware-configuration.nix

    ];

  # Bootloader.
  boot.loader.systemd-boot.enable = true;
  boot.loader.efi.canTouchEfiVariables = true;

  networking.hostName = "endernix"; # Define your hostname...
  # Enable networking
  networking.networkmanager.enable = true;

  # Enable docker
  virtualisation.docker.enable = true;

  # Enable bluetooth
  hardware.bluetooth.enable = true;
  hardware.bluetooth.powerOnBoot = true;
...
}
```

The comments above each line or chunk of code describe their functionality. For example, the Bluetooth chunk describes that when re-building the system again, it needs to enable and start the bluetooth service on boot. We'll get into rebuilds later on, but how do we install packages? Easy. we declare it in the same file.  

```nix
{ ...
users.users.ifkash = {
    isNormalUser = true;
    description = "Kashif";
    extraGroups = [ "networkmanager" "wheel" "docker" ];
    packages = with pkgs; [
      # Browsers
      brave
      firefox
      google-chrome
      # Fetch tools
      neofetch
      sysfetch
      nitch
    ];
};

...
}
```

Now these blocks can be placed anywhere in the file, because Nix is a purely functional programming language, which in layman's terms mean that positions of definitions does not matter sequentially.

## Reproducibility

Once our system's file has been configured, it's time to build/modify our system. Running `sudo nixos-rebuild switch` will read the entire configuration file and build a new Nix system accordingly. Now comes the question, would it take nearly double the size of the previous version if i simply include small packages in the new rebuild? The answer is No.

### /nix/store

Nix store is a location where Nix system stores all the names of the packages in the form of files with their dependency list hashed and attached to the file name. This way, whenever the system is rebuilt, if it is available in nix store, it is simply ignored. If not, a new file is created in nix store and added with appropriate rules.

We can also go back to our previous build with \``nixos-rebuild --rollback switch`

### Rollbacks - Never break your system again

Hence, incase our new system breaks for some reason, we can always switch back to the previous version and get our work done. This feature gives it the deadly advantage against distros like Arch Linux.

## Immutability

Since the system is defined declaratively, it's not possible to modify the system's existing state (like updating/upgrading packages, etc) This is not a bug, but a feature. It enables further safety against breaking our systems. This also means we cannot install additional things into the system in the current rebuild. It also makes the system more secure against attacks that intend to change ownership permissions or corrupt the boot files of the system.

## The Nix package manager

The Nix package manager fetches from the Nix package repository, one of the largest repos among all operating systems, it even beats Arch's user repository well known for its enormous package support. Hence, Nix boasts better software support than most operating systems on the planet.

You can search your favorite packages here: [https://search.nixos.org/packages](https://search.nixos.org/packages)

## Why use NixOS as a daily driver?

Apart from excellent software support, and all its other features. NixOS doesn't feel different from other Linux distros at all on the surface level. There's that feel-at-home and works-out-of-the-box feeling. Now that NixOS's installation ISO comes with the graphical calamares installer, it makes installing it even easier.

## Acknowledgements

* [https://nixos.org/](https://nixos.org/)
    
* [https://github.com/kashifulhaque/nixos-config](https://github.com/kashifulhaque/nixos-config)
    
* [https://ianthehenry.com/posts/how-to-learn-nix/](https://ianthehenry.com/posts/how-to-learn-nix/)
    
* [https://www.youtube.com/@vimjoyer](https://www.youtube.com/@vimjoyer)