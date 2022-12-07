## Install and Configure Telnet

FYI: Telnet is not secure. The passwords are transferred using plain text.

Check if telnet package already installed:
```shell
$ rpm -qa | grep telnet
```

If not, install 2 packages:
```shell
$ yum install telnet-server telnet
```

Add service to firealld:
```shell
$ firewall-cmd --add-service=telnet --zone=public
```

Add service to selinux:
```shell
$ semanage port -a -t telnetd_port_t -p tcp <port>
```

Enable and start service:
```shell
$ systemctl start telnet.socket
```

Test from client:
```shell
$  telnet <server>
```