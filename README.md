Role Name
=========

This Ansible role provisions a applications and sets up the dock on a Mac OSX computer.

This role takes care of:

Installing the required applications;
Creating dock icons for the apps & folders of the user's preference.

Requirements
------------

This role uses homebrew to install apps, therefore homebrew must be installed prior to invoking the role. 

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

**dockapps_apps:** provides a list of apps that are to be installed and/or added to the dock. Each item describes up to three attributes: **cask**, **description** & **path** which are defined as follows:

~~~~
dockapps_apps:
	- { cask:		 < name of homebrew cask for installation of the app >,
	    description: < some words to describe the app >,
	    path:		 < path to app package for presentation on the dock >
~~~~

 **Note:** both **cask** & **path** are optional. If **cask** is specified then dockapps will use homebrew to install the app. If **path** is specified then dockapps will add the app to the dock. By making these optional one may just install but not dock an app, or dock an app that has been installed by another process (e.g. a manual install or from Apple Store).

e.g.
~~~~
	# Install & place on dock
    - { cask: google-chrome,
        description: "A fast, free web browser. One browser for your computer, phone and tablet",
        path: "/Applications/Google Chrome.app" }

    # Place on dock, assumes already installed
    - { description: "iTerm2 brings the terminal into the modern age with features you never knew you always wanted.",
        path: "/Applications/iTerm.app" }

    # Install only, don't place on dock
    - { cask: colorpicker-skalacolor,
        description: "An extraordinary color picker for designers and developers" }

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
