# Directions for setting up a reverse ssh tunnel as a systemd service in Linux

We assume that we have full access to a server (from now SSH server) and we want to get SSH access to a computer behind a firewall (from now client).

We also assume that the operating system is a Linux system which runs systemd services
## Steps:
1. Generate an id_rsa key using the `ssh-keygen` command.
2. Copy the generated `id_rsa.pub` file to the SSH server .
3. Add the line from the file sshd_config_edit to the end of the sshd_config file of your SSH server.
4. Edit the file rtunnel.service to contain the correct information and add it in the folder /etc/system/systemd/
5. Run as root the command `systemctl daemon-reload`
6. Start the service with the command `service rtunnel start`
7. Connect to the client by issuing the command `ssh -p 2225 remote.host.com` where `2225` is a port of your choice and `remote.host.com` is the SSH server.

## Debuging 

To debug run the command   `/usr/bin/autossh -M 0 -f  -N  -i /path/to/.ssh/id_rsa -R 2225:localhost:22 -l username  remote.host.com` from the rtunnel.service file without the `-f` flag.

## Exlplanation of flags

* -M 0 : do not monitor
* -f   : run in the background
* -N   : do not do anything after connecting
* -l   : username (should be the same as the username appearing in the id_rsa and id_rsa.pub file )
* -i   : path to authentication file
* -R   : port forwarding. Forwards the port 2225 to the port 22 in the localhost. 

## Explanation of parameters:

* username: the username mentioned in the id_rsa files.
* remote.host.com: the SSH server
* 2225 the port you want to use  to forward the 22 port of your client 



