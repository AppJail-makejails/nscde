# nscde

NsCDE is a retro but powerful UNIX desktop environment which resembles CDE look (and partially feel) but with a more powerful and flexible framework beneath-the-surface, more suited for 21st century unix-like and Linux systems and user requirements than original CDE.

NsCDE can be considered as a heavyweight FVWM theme on steroids, but combined with a couple other free software components and custom FVWM applications and a lot of configuration, NsCDE can be considered a lightweight hybrid desktop environment.

github.com/NsCDE/NsCDE

![nscde logo](https://github.com/NsCDE/NsCDE/raw/master/NsCDE.png)

## How to use this Makejail

```
INCLUDE options/network.makejail
INCLUDE gh+AppJail-makejails/nscde

OPTION copydir=files
OPTION file=/etc/rc.conf
OPTION x11
```

Where `options/network.makejail` are the options that suit your environment, for example:

```
ARG network
ARG interface=nscde

OPTION virtualnet=${network}:${interface} default
OPTION nat
```

The tree structure of the `files/` directory is as follows:

```
# tree -pug files/
[drwxr-xr-x root     wheel   ]  files/
└── [drwxr-xr-x root     wheel   ]  etc
    └── [-rw-r--r-- root     wheel   ]  rc.conf

1 directory, 1 file
```

Where `rc.conf` is your custom `rc.conf(5)` file, for example:

```
clear_tmp_X="NO"
```

The `rc.conf(5)` file above sets `clear_tmp_X` to `NO` to not remove the sockets and various related files before the jail starts.

Open a shell and run `appjail makejail`, `appjail start` and `appjail run`:

```sh
appjail makejail -j nscde -- --network development
appjail start nscde
appjail run nscde
```

`xephyr` is very useful for using these applications.

```
Xephyr -screen 900x640 -br -ac -noreset :1 &
appjail run -p 'display=:1' nscde
```
