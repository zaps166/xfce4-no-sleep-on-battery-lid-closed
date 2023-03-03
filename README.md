# xfce4-no-sleep-on-battery-lid-closed

## Description

This tool prevents suspend if you have external display connected when running on laptop's battery in Xfce4 desktop

## Installation (Linux)

```sh
git clone https://github.com/zaps166/xfce4-no-sleep-on-battery-lid-closed.git
cd xfce4-no-sleep-on-battery-lid-closed
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr
make
sudo make install/strip
```

---

It's available in [AUR](https://aur.archlinux.org/packages/xfce4-no-sleep-on-battery-lid-closed-git)
