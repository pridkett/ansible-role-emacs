Emacs - Patrick's Fancy Emacs Role
==================================

Patrick Wagstrom &lt;patrick@wagstrom.net&gt;

May 2020


Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

- `emacs.install_zsh`: Whether or not a file `emacs.zsh` should be dropped into `~{{ ansible_env.HOME }}/.zsh.d` to allow for easier 24 bit color startup.
- `emacs.install_bash`: Whether or not a file `emacs.sh` should be dropped into `~{{ ansible_env.HOME }}/.bash.d` to allow for easier 24 bit color startup.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

MIT

Author Information
------------------

Patrick Wagstrom &lt;patrick@wagstrom.net&gt;
