# Run GUI on Mac OS X

Taken from:

- https://stackoverflow.com/questions/37523980/running-gui-apps-on-docker-container-with-a-macbookpro-host/51119072

On a Mac you may find the following steps useful:

1. Install XQuartz
2. Open it, goto preferences > Security and check the option to allow connections from network clients
3. Reboot
4. Start XQuartz (from the applications folder or with `open -a XQuartz`)
5. Allow incoming connections from your ip with `xhost + $IP` (see note 1)
6. Run firefox in your docker container (see note 2)

_Note 1:_ Here's a neat trick to get your ip address:

`export IP=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')`

_Note 2:_ And an example docker run command to start firefox:

`docker run -it -e DISPLAY=$IP:0 -v /tmp/.X11-unix:/tmp/.X11-unix <image> firefox`

Make sure to share `/private/tmp/` on Docker Desktop first:

`docker run --net host --rm --name firefox -e DISPLAY=$IP:0 -v /private/tmp/.X11-unix:/tmp/.X11-unix jess/firefox`

`docker run --net host --rm --name notepad -e DISPLAY=$IP:0 -v /private/tmp/.X11-unix:/tmp/.X11-unix wine-64-install notepad`
`docker run --net host --rm --name notepad -e DISPLAY=$IP:0 -v /private/tmp/.X11-unix:/tmp/.X11-unix wine-x86-64-install notepad`
`docker run --net host --rm --name notepad -e DISPLAY=$IP:0 -v /private/tmp/.X11-unix:/tmp/.X11-unix wine-x86-install notepad`

# Apps being started outside the Desktop limits?

Bring them back following the steps described by "Try Window Zoom":

- http://osxdaily.com/2013/08/14/move-window-back-on-screen-mac-os-x/
