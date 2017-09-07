## Install Docker 

https://docs.docker.com/engine/installation/linux/centos/

## Upload/copy certs rar on VM
		
``` 
scp -i <key path> <rar file path>  user@<ip>:/user/
```

### Install unrar  

```
wget ftp://ftp.pbone.net/mirror/ftp5.gwdg.de/pub/opensuse/repositories/home:/Kenzy:/modified:/C7/CentOS_7/x86_64/unrar-5.0.12-2.1.x86_64.rpm
```
```
rpm -Uvh unrar-5.4.5-1.el7.x86_64.rpm
```
```
unrar e \certs.rar
```

### Replace ExecStart with below line in file /usr/lib/systemd/system/docker.service

```
ExecStart=/usr/bin/dockerd --selinux-enabled --tls=true --tlscacert=/root/ca.pem --tlscert=/root/server-cert.pem --tlskey=/root/server-key.pem -H tcp://0.0.0.0:2376
```

### Disable firewall
```
systemctl disable firewalld
```

### Add below lines in .bashrc

```
  export DOCKER_TLS_VERIFY="1"
  export DOCKER_HOST="tcp://localhost:2376"
  export DOCKER_CERT_PATH="/root"
```
```
source .bashrc
```

### Restart docker
```
systemctl daemon-reload
```
```
service docker restart
```
