# spideroak-systemd

**Work in Progress**

This project provides the systemd unit file for starting and stopping the
SpiderOak service (https://www.spideroak.com) from a systemd environment. This
is based off the work done by funnelfiasco
(https://github.com/funnelfiasco/spideroak-init).

This repository includes the following files:
* COPYING.md         -- the license (public domain where applicable, 
                        CC0 elsewhere) 
* README.md          -- this file
* `install.sh`         -- install script (*just for convenience*)
* `.spideroak.rc`      -- the configuration file
* `spideroak`          -- the systemd script which deal with applying the
                          configuration from `.spideroak.rc`
* `spideroak@.service` -- the systemd service file

## Installation
### Automatically
Just run `./install.sh` directly from the git repo, all the files *should*
be copied over. **This needs root privileges!**

### Manually
To install on a system using systemd, copy the file 'spideroak@.service' to
`/usr/lib/systemd/system/spideroak@.service`, copy `spideroak` to
`/usr/lib/systemd/script/spideroak`, and the file `.spideroak.rc` to
`~username/.spideroak.rc`. 

## Configuration
Configuration is handled through `~username/.spideroak.rc`. The systemd
service will use the `ARG` variable to pass options to the SpiderOak
process. '--headless' is automatically included and so does not need to be
specified in `ARG`.

**Note: the scripts and configuration do not perform any sanity-checking
on your behalf. For the security of your system and data, ensure that files
have the proper ownership and permissions.**

## Multi-user support
For systemd, the provided service file is a template. The text between the 
@ and . Indicate the user name that SpiderOak should be launched as. Thus
to start SpiderOak for both user 'funnel' and user 'fiasco' you would run

    systemctl spideroak@funnel.service start
    systemctl spideroak@fiasco.service start

Setting per-user SPIDEROAKOPTS is not currently supported.
