# Fake EON

The purpose of this Docker container is to mimic the SSH setup of the EON as closely as possible.
It even includes freshly cloned Openpilot code in `/data/openpilot`.

We created this to test Workbench without an EON needing to be present.
Also, we could theorhetically run more than one of these to test multi-EON results in scans.

This will also be used to test the new Openpilot Editor that will be built within Workbench soon.

## Usage

To get started, install Docker on your Mac, Windows, or Linux machine.
Not going to cover this as its very easy to install.

Now clone this repo to your computer...

`git clone https://github.com/openpilot-community/opc-fake-eon.git ~/MyProjectsDirectory/opc-fake-eon`

Change into that directory...

`cd ~/MyProjectsDirectory/opc-fake-eon`

Build the docker container...

`docker-compose build`

Start the docker container...

`docker-compose up`

You should now see something like the following:

```sh
opc-fake-eon % docker-compose up
Starting opc-fake-eon_server_1_ff1733ad9450 ... done
Attaching to opc-fake-eon_server_1_ff1733ad9450
server_1_ff1733ad9450 |
server_1_ff1733ad9450 | ---> Starting the SSH server.
server_1_ff1733ad9450 | Starting OpenBSD Secure Shell server: sshd.
server_1_ff1733ad9450 | sshd is running.
```

Now switch to a new tab in your Terminal emulator and test it out...

`ssh root@0.0.0.0 -p 8022 -i ~/.ssh/openpilot_rsa`

If you already had your openpilot_rsa key setup from using Workbench, this should all be successful and return something similar to below...

```sh
opc-fake-eon % ssh root@0.0.0.0 -p 8022 -i ~/.ssh/openpilot_rsa
Last login: Tue Feb 12 23:08:47 2019 from 172.22.0.1
root@server:/system/comma/home#
```