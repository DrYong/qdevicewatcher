QDeviceWatcher can detect usb storage add and remove event.
Tested on linux (>= 2.6), windows(mingw and msvc) and OSX(buggy).

License under LGPL 2.1 or later

Screenshot
-----

![Alt text](https://github.com/wang-bin/qdevicewatcher/raw/master/screenshot/ubuntu.png              "Ubuntu non-debug")
![Alt text](https://github.com/wang-bin/qdevicewatcher/raw/master/screenshot/ubuntu-gui-debug.png    "Ubuntu gui debug")
![Alt text](https://github.com/wang-bin/qdevicewatcher/raw/master/screenshot/win7.png                "Win7 non-debug")
![Alt text](https://github.com/wang-bin/qdevicewatcher/raw/master/screenshot/win7-gui-debug.png      "Win7 gui debug")
![Alt text](https://github.com/wang-bin/qdevicewatcher/raw/master/screenshot/wince-emu-gu.png        "WinCE emulater")

Add by Yong:
from : https://forum.qt.io/topic/9382/qdevicewatcher-make-hotplug-detection-easy

It's my project: https://github.com/wang-bin/qdevicewatcher
Just need QtCore module.
It works fine on linux and windows. I have tested on my ubuntu and win7. Usually you just need the signals @deviceAdded(const QString& device)@ and @deviceRemoved(const QString& device)@ in QDeviceWatcher.

To detect the device changes, i use netlink in linux(kernel 2.6) and internel window in windows.
In windows, I tried two method,
@virtual bool QCoreApplication::winEventFilter(MSG* msg, long* result)
//and
virtual bool QWidget::winEvent(MSG* msg, long* result)@
I hope my class is just a subclass of QObject, and do not use GUI module, so I started to find other ways. At last I refer to qdrive project: https://gitorious.org/qdrive/qdrive
In qdrive project, it watch /etc/mtab in linux, but some systems will not mount new disk, so I use netlink.
This class is only for watching hotplug events now. You can deal with the device yourself, e.g. mount and umount the device.
