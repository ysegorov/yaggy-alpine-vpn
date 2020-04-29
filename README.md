# alpine-vpn


## Installation

1. Install [Alpine Linux][alpine-install] in [sys mode][alpine-sys-mode].
2. Configure mirror if needed (check [mirrors.yaml][alpine-mirrors]
   for available mirrors):
  - check/update `/etc/apk/repositories`
  - run `apk update` to update apk repository indexes
  - run `apk upgrade` to upgrade outdated packages
3. Install `sudo`:
  - `apk add sudo`
  - allow `wheel` group users to run passwordless `sudo` commands (edit
      `/etc/sudoers` file using `visudo`)
4. Add [new user][alpine-new-user] account for management:
  - add/edit defaults in `/etc/skel`
  - add new user group using `addgroup groupname`
  - add new user account using `adduser -D -G groupname --shell /bin/ash username`
  - add newly created account to `wheel` group using `addgroup username wheel`
  - set password for newly created account using `chpasswd`
  - create `.ssh` dir using `mkdir $HOME/.ssh` and `chmod 700 $HOME/.ssh`
  - place OpenSSH public key to `$HOME/.ssh/authorized_keys` file
  - set proper authorized keys file permissions using `chmod 600 $HOME/.ssh/authorized_keys`
5. Configure OpenSSH daemon (`/etc/ssh/sshd_config`):
  - customize port
  - specify allowed users
  - disable login using password
  - disable root account login
  - restart `sshd` using `service sshd restart`


## Configuration

TODO


## Notes

- `unbound` is very sensitive to local server datetime, it must be correct for
    proper DNSSEC validation


[alpine-install]: https://wiki.alpinelinux.org/wiki/Installation
[alpine-sys-mode]: https://wiki.alpinelinux.org/wiki/Alpine_newbie_install_manual#sys_mode
[alpine-new-user]: https://wiki.alpinelinux.org/wiki/Alpine_newbie_apk_packages#New_users:_management_of_users_and_logins
[alpine-mirrors]: https://git.alpinelinux.org/aports/tree/main/alpine-mirrors/mirrors.yaml
