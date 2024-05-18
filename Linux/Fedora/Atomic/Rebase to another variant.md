First you need to pin the last deploy for security reasons:
```
sudo ostree admin pin 0
```

After this, search to desired variant using this command:
```
ostree remote refs fedora
```

If needed, you can unpin some deploy using:
```
sudo ostree admin pin --unpin 2
```

Then, change to new variant:
```
rpm-ostree rebase fedora:fedora/40/x86_64/kinoite
```

**Important:** Be careful about distro version and arch!

---
To undo this, you can reboot you machine and press "shift" before OS boot and choose the previous variant on menu. Then, after boot on a terminal run:
```
rpm-ostree rollback
```