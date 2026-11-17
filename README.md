# Install TigerVNC Server and a lightweight desktop environment (XFCE works reliably over VNC):
```console
sudo apt update
sudo apt install -y tigervnc-standalone-server xfce4 xfce4-goodies dbus-x11
```

# setup VNC login Password
```console
vncpasswd
```

# create startup
```console
mkdir -p ~/.config/tigervnc

cat << 'EOF' > ~/.config/tigervnc/xstartup
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
exec dbus-launch --exit-with-session startxfce4
EOF

chmod +x ~/.config/tigervnc/xstartup
```

# Clean the residule and restart VNC
```console
vncserver -kill :1 2>/dev/null
vncserver :1 -geometry 1920x1080 -depth 24
```

# On Clinet side, set up the ssh link tunnel
```console
ssh -L 5901:127.0.0.1:5901 -N -f hostpxe@192.168.100.100
```

# Install TigerVNC Client and Open Tiger VNC Viewer to login dashboard
localhost:5901
