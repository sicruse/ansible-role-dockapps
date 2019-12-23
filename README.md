Role Name
=========

This Ansible role sets up the dock on a Mac OSX computer. It takes care of creating dock icons for the apps & folders of the user's preference.

Requirements
------------

This role uses [dockutil](https://github.com/kcrawford/dockutil|dockutil) to manipulate the dock and will install this via homebrew. Therefore homebrew must be installed prior to invoking the role.

~~~~
########### Install Homebrew ############
if ! command -v brew >/dev/null; then
  echo Installing Homebrew...
  # supress the need to press 'return' when in the install script runs.
  yes '' | ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
else
  echo Homebrew already present...
fi
~~~~

Role Variables
--------------

**dockapps_apps:** provides a list of apps that are to be added to the dock. Each item describes the application **path** defined as follows:

~~~~
dockapps_apps:
	- < path to app package for presentation on the dock >
~~~~

e.g.
~~~~
	# Install & place on dock
    - "/Applications/Google Chrome.app"
~~~~

**dockapps_folders:** provides a list of folders, including the preferred view mode, to include on the dock. e.g.

~~~~
dockapps_folders:
    - { path: "~/Downloads",  view: fan   }
    - { path: "~/Documents",  view: grid  }
~~~~

Dependencies
------------

This role has no other ansible galaxy dependencies.

Example Playbook
----------------

	---
	- hosts: localhost
	  remote_user: root
	  roles:
	    - sicruse.dockapps

License
-------

MIT

Author Information
------------------

If you have any questions or comments feel free to reach me via [email](mailto:si@sicruse.com?subject=dockapps Feedback)
