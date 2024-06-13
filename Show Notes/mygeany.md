Modified Geany Configuration
============================

## Table of Contents

- [Initial Setup](#setup)
- [Geany Plugins](#plugins)
- [Installation](#installation)
- [Usage](#usage)
- [Conclusion](#conclusion)

##  Initial Setup

![2024-06-13_14-43](https://github.com/drewgrif/documentation/assets/11249871/d2e718bb-a9af-4264-a0b1-435fc4983b6d)
![2024-06-13_14-44](https://github.com/drewgrif/documentation/assets/11249871/201415fe-d9ad-467d-bfc2-1a7211af3b8e)
![2024-06-13_14-46](https://github.com/drewgrif/documentation/assets/11249871/03c633a3-7e68-4454-b9aa-d7e69f1fb82f)
![2024-06-13_14-48](https://github.com/drewgrif/documentation/assets/11249871/fa04443b-966f-412d-bd93-f58f1522d5f1)
![2024-06-13_14-50](https://github.com/drewgrif/documentation/assets/11249871/8326cf6c-5ccb-4b11-b711-a183ac190b64)
![2024-06-13_14-51](https://github.com/drewgrif/documentation/assets/11249871/fd661c7d-3e63-4e42-941a-4e5f23d831eb)
![2024-06-13_14-53](https://github.com/drewgrif/documentation/assets/11249871/31535693-c6b3-4f0b-9774-37980189e55d)

## Geany Plugins
Install these plugins

1. [geany-plugin-addons](#geany-plugin-addons)
2. geany-plugin-git-changebar 
3. geany-plugin-markdown
4. geany-plugin-spellcheck 
5. geany-plugin-treebrowser 
6. geany-plugin-vimode (availabe/optional) 
7. Split Window (installed by default)

### geany-plugin-addons
NOTE: I like the hover 



## Installation

```
sudo apt install \
    python3 \
    python3-pip \
    python3-venv \
    python3-v-sim \
    python-dbus-dev \
    libpangocairo-1.0-0 \
    python3-cairocffi \
    python3-xcffib \
    libxkbcommon-dev \
    libxkbcommon-x11-dev \
    git \
    sxhkd

```
Make sure:

1. You have a ~/.local/bin directory
2. You have the following in your .bashrc

```
export PATH="~/.local/bin:$PATH"

```

### Setting Up Virtual Environment

```
python3 -m venv ~/.local/src/venv
```

### Using qtile.git
```
git clone https://github.com/qtile/qtile.git ~/.local/src/venv/qtile

```

### Installing qtile 
```
~/.local/src/venv/bin/pip install ~/.local/src/venv/qtile/.

```
### Installing psutil
```
~/.local/src/venv/bin/pip install psutil

```
### Setting symbolic link
```
ln -sf ~/.local/src/venv/bin/qtile ~/.local/bin/

```

## Usage

```
sudo nano /usr/share/xsessions/qtile.desktop

```

Paste the following.  Change $USER.
```
[Desktop Entry]
Name=Qtile
Comment=Qtile session
Exec=/home/$USER/.local/bin/qtile start
Type=Application
Keywords=wm;tiling

```

## Conclusion

By the end you should be able to log into vanilla qtile.
