### git portage sync

by default, portage uses rsync. some users may find this to be rather slow, or their habit of checking for updates resulted in a temporary ban from rsync.

first of all, install `dev-vcs/git`, if you haven't already. ***it is required***

create the text file `/etc/portage/repos.conf/default.conf`

```ini
[DEFAULT]
main-repo = gentoo
```

which defines the main repository, which is obviously gentoo

choose your variant of git sync [verified](#verified-sync), or [unverified](#unverified-sync).

### verified sync

create the text file `/etc/portage/repos.conf/gentoo.conf`

```ini
[gentoo]
auto-sync = yes
location = /var/db/repos/gentoo
sync-git-verify-commit-signature = yes
sync-depth = 1
sync-openpgp-key-path = /usr/share/openpgp-keys/gentoo-release.asc
sync-type = git
sync-uri = https://github.com/gentoo-mirror/gentoo.git
```

which will verify the commit signature of the *lastest* commit aginst gentoo's pgp keys each time the repository is updated

now [complete the setup](#complete-the-setup), or continue reading the other option...

### unverified sync

create the text file `/etc/portage/repos.conf/gentoo.conf`

```ini
[gentoo]
auto-sync = yes
location = /var/db/repos/gentoo
sync-depth = 1
sync-type = git
sync-uri = https://github.com/gentoo-mirror/gentoo.git
```

which will not verify any commit signatures!

### complete the setup

remove the current gentoo repository as portage cannot clone the git repository into the non-empty directory

```shell
# rm -rf /var/db/repos/gentoo
```

and sync the gentoo repository

```shell
# emerge --sync gentoo
```

### extra info

the `sync-depth` option translates to git's `--depth=` option, which performs [shallow clones and fetches](https://www.git-scm.com/docs/shallow). a value of `0` is equivalent to omitting this option, aka fetch the **full** history
