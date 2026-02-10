#Upgrades, People, Upgrades!

This entry has instructions for how to check my VM for updates, and how to install them!

Steps:
- sudo apt update (this will fetch the newest version of the packages in the VM)
- apt list --upgradable (this lists all of the packages that need to be upgraded. If there are none, stop here)
- sudo apt upgrade (this will install the new versions that we just retreived)
- sudo apt update ; apt list --upgradable (this last step runs 1&2 to check that everything worked!)