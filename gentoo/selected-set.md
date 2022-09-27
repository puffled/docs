### the `@selected` set

a selection of packages which you have requested to be installed, and remain installed.

they are stored in a plain text file located at `/var/lib/portage/world`, (yes it is `world`. it is not `selected`.)

each entry is on their own line in the form `category/package`.

you may safely remove items from this set via `emerge --deselect <packages...>`, or by manually editing `/var/lib/portage/world`, followed by an `emerge --depclean --pretend`, and possibly `emerge --depclean`, if the former will remove as you desired.

you may ***less*** safely remove items from this set via `emerge --unmerge`, ***it will not check dependencies***. only use this if you ***really*** wish to remove a package.
