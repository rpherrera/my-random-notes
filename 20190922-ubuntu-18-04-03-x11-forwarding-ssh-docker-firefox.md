
# Server Steps

## Required: Ubuntu 18.04.3 LTS

1. Install `xorg` packages:

```
sudo apt-get install xorg
````

2.1. Make sure you have X11 Forwarding activated:

```
grep X11Forwarding /etc/ssh/sshd_config
````

2.2. Expected result:

```
X11Forwarding yes
```

# Client Steps

1. Get logged into your server by enabling a trusted X11 Forwarding (flag `-Y`):

```
ssh -Y user@server-host
````

2. Run Firefox as a Docker container, inside the server, sharing its `.Xauthority` file and the virtual display, so X11 should be Forwarded by means of SSH and you should see it on the client side:

```
docker run \
  --rm \
  --detach \
  --name firefox \
  --net=host \
  --env DISPLAY \
  --volume="$HOME/.Xauthority:/root/.Xauthority:rw" \
  jess/firefox
```
