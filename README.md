# suse-csb-release

## Project Description
SUSE IT needs help from fellow geekos with release engineering skills to define the requirements, process, infrastructure, and tools for building an openSUSE-based distribution bundled with SUSE IT-supported application stack. The resulting OS build will be offered as a standard distribution for new SUSE employees in addition to the existing Operating System library.

## Goal for this Hackweek
* Define requirements (and name) for the build.
* Selected features implemented for the MVP.
* Define a process for updating the image with the future releases of openSUSE.
* Identify and deploy required infrastructure and repositories.
* Produce an installable OS image that can be used by volunteers across the company.
* Document everything.
* Have a lot of fun in the process.

## MVP requirements
* the deployment do the end-user machine is unattended
* machine has disk encrypted
* once the machine is provisioned, it is added to asset DB (serial number + asset owner)
* productivity tools are installed
* Details are tracked here: https://en.opensuse.org/Portal:Leap:CSBRequirements


## Combustion example usecase for SUSEIT

About combustion https://en.opensuse.org/Portal:MicroOS/Combustion

### What does our combustion example?
* set root password (by default unset)
* enforce that user has to specify root password while using sudo (root access controlled by SUSE IT)
* change the default btrfs/luks password (set to suse-it by default). This part doesn't work for some reason.

### Firstboot wizzard for user
**The rest of the configuration will be done by the user as part of the first boot. This is handled by gnome-initial-setup.**

Once the gnome-initial-setup is finished and network connectivity is established, additional SUSE-it pre-selected non-rpm software will be deployed via mod-firstboot. This is handled by gnome-branding-Leap.

### Instructions for SUSE IT###
Copy combustion directory from this git repo on a root of flash drive formatted as ext4 disk has to be labeled as "ignition".

Tweak password for luks and root in the config script on the USB drive.

**Ensure that the USB drive is plugged on the first boot to the employee machine.**

The machine will be rebooted afterward due to a one-shot reboot service (livecd/openSUSE/config.sh).

Perhaps you could do what Vadim did with fido?

TODO: do not print debug output into /etc/issue.d/combustion

### Credit

Big thanks to Richard Brown and his work on MicroOS, as this is heavily based on his setup.
