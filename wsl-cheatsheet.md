### wsl Help
wsl --help

# Check WSL status
wsl --status

# Check WSL version
wsl --version

# Update WSL
wsl --update

# To list installed distributions (The default version of distro is explicitly mentioned in paranthesis)
wsl -l
wsl --list

# See a list of the Linux distributions available through the online store
wsl -l -o
wsl --list --online

# To list installed distributions along with its running status and wsl config being 1 or 2 
# The default version of distro is explicitly marked with prefix `*` before its name
wsl -l --verbose
wsl -l -v

# Set default WSL version
wsl --set-default-version <Version>

# To run a specific distro
wsl -d distro_name
wsl --distribution distro_name

# To terminate/shutdown a specific distro
wsl -t distro_name_to_shutdown
wsl --terminate distro_name_to_shutdown

# To shutdown all disstros
wsl --shutdown

# Set specific distro as default
wsl -s my_default_distro
wsl --set-default my_default_distro

# To EXPORT a running distro as image (Defaults to tar format)
wsl --export distro_name_to_export windows_path\tar_file_name.tar

# To EXPORT a running distro as image in vhd format (only supported using WSL 2)
wsl --export distro_name_to_export --vhd windows_path\tar_file_name.vhd

# To IMPORT an image as distro
wsl --import new_distro_name install_location_windows_path tar_file_name.tar --version wsl-version-1-or-2
wsl --import Ubuntu-20 D:\VMs\WSL\Ubuntu-20\ Ubuntu-20.04.tar --version 2 # Setting my secondary HDD as storate loc for new distro
wsl --import Ubuntu-20 --vhd D:\VMs\WSL\Ubuntu-20\ Ubuntu-20.04.vhd --version 2 # Importing distro in vhd format

# To UNREGISTER (also removes the its file storage) a distro
wsl --unregister distro_name_that_delete

# To run a WSL distro as the specified user.
wsl -u username -d distroname
wsl -u root -d Ubuntu-20.04

# To change the default user for a distribution
DistributionName config --default-user Username
ubuntu config --default-user my_default_username
ubuntu2004.exe config --default-user johndoe # When you have Ubuntu 20.04 version installed from the Microsoft Store

# Identify IP address of your Linux distribution installed via WSL 2 (the WSL 2 VM address)
wsl hostname -I

# Identify IP address of the Windows machine as seen from WSL 2 (the WSL 2 VM)
ip route show | grep -i default | awk '{ print $3}'

# Shink WSL disk space manually
# WSL disk space grows automatically but doesn't shrink automatically. You got to shrink it after shutting the disk down like below.
# Open windows terminal in administrator mode
# cd directory-where-your-wsl2-distro-is-located
cd D:\VM\WSL\Ubuntu
wsl -l -v
wsl --shutdown your-distro-name 
# without the distro name it will shutdown all distros and if you got DockerDesktop running, it will be shutdown as well
Optimize-VHD -Path .\ext4.vhdx -Mode full


# List of deprecated WSL Commands
# These commands were the original wsl syntax for configuring Linux distributions installed with WSL, but have been replaced with the wsl or wsl.exe command syntax.
wslconfig.exe [Argument] [Options]
bash [Options]
lxrun /[Argument]
