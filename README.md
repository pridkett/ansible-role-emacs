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
- `emacs.install_from_head`: Whether or not emacs should be installed from the `daviderestive/emacs-head` recipe in homebrew. Defaults to `False`.
- `emacs.build_flags`: Flags to pass to homebrew when building emacs. This is only used when `emacs.install_from_head` is `True`. If this is undefined and `emacs.install_from_head` is `True` then the bottled version of `daviderestivo/emacs-head@27` will be installed. In most cases, you should not need to set this variable. Setting it also makes it likely to break the recipe as the underlying recipe changes frequently.

Dependencies
------------

- [homebrew](https://docs.ansible.com/ansible/latest/modules/homebrew_module.html): needed for installing on MacOS

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
      build_from_head: true
      # build_flags: ["HEAD", "with-cocoa", "with-librsvg", "with-imagemagick", "with-no-frame-refocus", "with-mailutils", "with-dbus", "with-modules", "with-xwidgets"]
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

License
-------

MIT

Author Information
------------------

Patrick Wagstrom &lt;patrick@wagstrom.net&gt;
