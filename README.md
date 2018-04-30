# Directions for a reverse SSH tunnel

We assume that we have full access to a server (from now SSH server) and we want to get SSH access to a computer behind a firewall (from now client).

We also assume that the operating system is a Linux system which runs systemd services
Steps:

1. Add the line from the file sshd_config_edit to the end of the sshd_config file of your SSH server.

2. Edit the file rtunnel.service to contain the correct information and add it in the folder /etc/system/systemd/

3. Run as root the command `systemctl daemon-reload`

4. Start the service with the command `service rtunnel start`
