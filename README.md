# rTorrent

This image runs [rTorrent](https://github.com/rakshasa/rtorrent), a bittorrent client with a very low memory footprint.

[![](https://badge.imagelayers.io/existenz/rtorrent:latest.svg)](https://imagelayers.io/?images=existenz/rtorrent:latest 'Get your own badge on imagelayers.io')

It makes use of the `runas` functionality found in [my base image](https://hub.docker.com/r/existenz/base/) so rTorrent runs as the user you want.

## Usage

To run rTorrent as a service under user id 1234 with group id 2345 start like this:

```
docker run -d -t \
-e UID=1234 -e GID=2345 \
-v /dir/.rtorrent.rc:/home/.rtorrent.rc \
-v /storage/torrents:/data \
-p 5000:5000
-p 6000:6000
existenz/rtorrent
```

## Alternative approach

The example above just mounts the .rtorrent.rc, and uses the pre-created dir /home/session in the image for storing session data.
To store the session data outside the image, mount a complete directory with both .rtorrent.rc and session on /home.
Whether your rTorrent actually uses session data is depending on your config file of course.

## Mapping ports

The image exposes no ports by default, because what ports you want to use depends on your configuration.
Just map the ports you use, in the example I used 5000 voor the SCGI mount and 6000 for incoming torrent traffic.

## Bugs, questions, and improvements

If you found a bug or have a question, please open an issue on the GitHub Issue tracker. Improvements can be sent by a Pull Request against the develop branch and are greatly appreciated!

