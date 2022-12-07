## Configuring SSH

#### Hardening SSH Server
* Disable root login
* Disable password login
* Configure a non-default port for SSH to listen on
* Allow specific users only to log into SSH 


#### Limit Root Access

SSH servers have root login enabled by default. This is the most serious security issue.

Disable root login by modifying PermitRootLogin parameter to *no* in **/etc/ssh/sshd_config**. Remember to restart service:
```shell
$ systemctl restart sshd
```

#### Alternate Ports

Port 22 is SSH default port.

Change port in **/etc/ssh/sshd_config**.

**Tip** To avoid being locked out of server after making a change to SSH listening port while remotely connected, open up two sessions to SSH server. Use one session to apply changes and test. The other session keeps current connection option. Active sessions are not disconnected after restarting the SSH server.

#### Modify SELinux for Port Change

Check if new SSH port already has a label:
```shell
$ semanage port -l <port>
```

If not, change label on non-default port:
```shell
$ semanage port -a -t ssh_port_t -p tcp <port>
```












#### End-of-Chapter Lab

1. Configure your SSH server in such a way that inactive sessions will be kept open for at least one hour.
2. Secure your SSH server so that it listens on port 2022 only and that only user lisa is allowed to log in.
3. Test the settings for server2. Make sure that the firewall as well as SELinux are configured to support your settings.