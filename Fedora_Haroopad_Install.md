# Haroopad Fedora Linux

Download the tarball from the official website
```
$ tar -zxvf haroopad-vx.x.x_amd64.tar
$ tar -zxvf data.tar.gz
$ sudo cp -r ./usr /
$ tar zxf control.tar.gz
$ chmod 755 postinst
$ sudo ./postinst
```

Verify Desktop file
`$ sudo vi /usr/share/applications/Haroopad.desktop`

Should look like
```
[Desktop Entry]
Name=haroopad
Version=0.13.1
Exec=haroopad
Comment=The Next Document processor based on Markdown
Icon=haroopad
Type=Application
Terminal=false
StartupNotify=true
Encoding=UTF-8
Categories=Development;GTK;GNOME;
```


Icons
`$ sudo cp -rf usr/share/icons/hicolor/ /usr/share/icons/hicolor`