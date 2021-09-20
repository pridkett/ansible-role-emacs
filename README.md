Emacs - Patrick's Fancy Emacs Role
==================================

Patrick Wagstrom &lt;patrick@wagstrom.net&gt;

May 2020

Requirements
------------

This package has no particular requirements. It should work on both MacOS and Linux (Ubuntu). On Ubuntu it will currently try to install a PPA to get newer versions of emacs and provide with support for inline images, xwidgets support, etc.

Role Variables
--------------

- `emacs.install_zsh`: Whether or not a file `emacs.zsh` should be dropped into `~{{ ansible_env.HOME }}/.zsh.d` to allow for easier terminal 24-bit color startup.
- `emacs.install_bash`: Whether or not a file `emacs.sh` should be dropped into `~{{ ansible_env.HOME }}/.bash.d` to allow for easier terminal 24-bit color startup.
- `emacs.install_fish`: Whether or not a file `emacs.fish` should be dropped into `~{{ ansible_env.HOME }}/.config/fish/fish.d` to allow for easier terminal 24-bit color startup.
- `emacs.config`: emacs-lisp code that will put near the end of `~/.emacs.d/init.el` but before `emacs.custom`. Functionally, this is used to distinguish between code blocks that may be overwritten by emacs customization and that which may not be overwritten.
- `emacs.create_initel`: Whether or not the script will try to create a templated `~/.emacs.d/init.el`. This defaults to `true`, set to `false` if you're going to be copying your configuration files from elsewhere.
- `emacs.custom`: emacs-lisp code that will be put at the end of `~/.emacs.d/init.el`. This is generally used for anything that was set up through emacs in-editor configuration. Placing it here means that additional changes will work with the same block of code.
- `emacs.copy_files`: a list of files to copy into your `~/.emacs.d/` directory. This is useful for when your configuration becomes really complicated and you want to use a completely custom `~/.emacs.d/init.el` or when you just need to copy a few files over.

Dependencies
------------

- [homebrew](https://docs.ansible.com/ansible/latest/modules/homebrew_module.html): needed for installing on MacOS
- [community.general](https://galaxy.ansible.com/community/general): needed to install the cask version of emacs-mac

Example Playbook
----------------

Here's an example playbook that will install emacs version 27 on MacOS from the `daviderestivo/emacs-head` tap. If you uncomment the `build_flags` line the you'll compile head from source.

In addition, this shows how you can add in arbitrary configuration settings and also add in packages that should be installed along with their configuration. You can use any of the named parameters for `use-package` (e.g. `after`, `hook`, `custom`, `config`, etc) with these to determine where code blocks should go in the generated `~/.emacs.d/init.el` file.

```yaml
- hosts: servers
  roles:
  - pridkett.emacs
  vars:
    emacs:
      install_zsh: true
      install_fish: true
      config: |-
        ;; Clean up the display some
        (if (fboundp 'tool-bar-mode)
            (tool-bar-mode -1))
        (if (fboundp 'scroll-bar-mode)
            (scroll-bar-mode -1))
      packages:
        - name: powerline
          config: (powerline-default-theme)
        - name: airline-themes
          config: |-2
            (load-theme 'airline-dark t)
```

Here's an alternate configuration that just copies configuration from a repository:

```yaml
- hosts: servers
  roles:
  - pridkett.emacs
  vars:
    emacs:
      create_initel: false
      install_zsh: true
      install_fish: true
      copy_files:
        - url: https://raw.githubusercontent.com/pridkett/org-wagstrom/main/org-wagstrom.el
          dest: org-wagstrom.el
        - url: https://raw.githubusercontent.com/pridkett/emacs.d/main/init.el
          dest: init.el
        - url: https://raw.githubusercontent.com/pridkett/emacs.d/main/config.org
          dest: config.org
```

License
-------

MIT

Author Information
------------------

Patrick Wagstrom &lt;patrick@wagstrom.net&gt;
