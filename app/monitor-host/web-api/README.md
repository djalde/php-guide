# Monitor API

- [Monitor Host](#monitor-host)

## Monitor Host

---

```
/?info=:info
```

**Params**

| Name  | Type   | Description      |
| ----- | ------ | ---------------- |
| :info | String | Name of resource |

**Examples**

[http://localhost:8080/v1/](http://localhost:8080/v1/):

```js
{
  "operatingSystem":"Ubuntu 14.04.5 LTS",
  "hostname":"vagrant-ubuntu-trusty-64",
  "username":"www-data",
  "uptime":"7 hours, 38 minutes"
}
```

[http://localhost:8080/v1/?info=nothing](http://localhost:8080/v1/?info=nothing):

```js
{
  "error":"Unknown info"
}
```

[http://localhost:8080/v1/?info=overview](http://localhost:8080/v1/?info=overview):

```js
{
  "operatingSystem":"Ubuntu 14.04.5 LTS",
  "hostname":"vagrant-ubuntu-trusty-64",
  "username":"www-data",
  "uptime":"7 hours, 40 minutes"
}
```

[http://localhost:8080/v1/?info=cpuStatus](http://localhost:8080/v1/?info=cpuStatus):

```js
{
  "cpuLast":{
    "last1":0,
    "last10":0.05,
    "last15":0.06
  },
  "cpuUsage":{
    "cpuUsageUser":0.3,
    "cpuUsageSys":0.2,
    "cpuUsageIdle":99.5
  }
}
```

[http://localhost:8080/v1/?info=cpuName](http://localhost:8080/v1/?info=cpuName):

```js
{
  "cpu":"Intel(R) Core(TM) i5-4250U CPU @ 1.30GHz"
}
```

[http://localhost:8080/v1/?info=memory](http://localhost:8080/v1/?info=memory):

```js
{
  "memoryUsageUsed":92.3,
  "memoryUsageUnused":7.7
}
```

[http://localhost:8080/v1/?info=users](http://localhost:8080/v1/?info=users):

```js
[
  {
    username: "root",
    encrypted_password: "x",
    uid: "0",
    gid: "0",
    gecos: "root",
    home: "/root",
    shell: "/bin/bash"
  },
  ...{
    username: "mysql",
    encrypted_password: "x",
    uid: "109",
    gid: "116",
    gecos: "MySQL Server,,,",
    home: "/nonexistent",
    shell: "/bin/false"
  }
];
```

[http://localhost:8080/v1/?info=services](http://localhost:8080/v1/?info=services):

```js
[
  {
    name: "tcpmux",
    port: "1",
    protocol: "tcp",
    description: "TCP port service multiplexer"
  },
  ...{
    name: "fido",
    port: "60179",
    protocol: "tcp",
    description: "fidonet EMSI over TCP"
  }
];
```

[http://localhost:8080/v1/?info=servicesStatus](http://localhost:8080/v1/?info=servicesStatus):

```js
[
  {
    service: "acpid",
    status: "up"
  },
  {
    service: "apache2",
    status: "up"
  },
  ...{
    service: "x11-common",
    status: "down"
  }
];
```

**Commands**

```sh
$ hostname
vagrant-ubuntu-trusty-64
```

```sh
$ whoami
vagrant
```

```sh
$  uptime -p
up 7 hours, 58 minutes
```

```sh
$ top -b -n 1
top - 12:28:57 up  7:58,  1 user,  load average: 0.00, 0.01, 0.05
Tasks:  85 total,   1 running,  84 sleeping,   0 stopped,   0 zombie
...
```

```sh
$ cat /proc/cpuinfo  | grep 'name'
model name      : Intel(R) Core(TM) i5-4250U CPU @ 1.30GHz
```

```sh
$ free
             total       used       free     shared    buffers     cached
Mem:        501692     465556      36136      19240      17172     261516
-/+ buffers/cache:     186868     314824
Swap:            0          0          0
```

```sh
$ cat /etc/services
# Network services, Internet style
#
# Note that it is presently the policy of IANA to assign a single well-known
# port number for both TCP and UDP; hence, officially ports have two entries
# even if the protocol doesn't support UDP operations.
#
# Updated from http://www.iana.org/assignments/port-numbers and other
# sources like http://www.freebsd.org/cgi/cvsweb.cgi/src/etc/services .
# New ports will be added on request if they have been officially assigned
# by IANA and used in the real-world or are needed by a debian package.
# If you need a huge list of used numbers please install the nmap package.

tcpmux          1/tcp                           # TCP port service multiplexer
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
systat          11/tcp          users
daytime         13/tcp
daytime         13/udp
netstat         15/tcp
qotd            17/tcp          quote
msp             18/tcp                          # message send protocol
msp             18/udp
chargen         19/tcp          ttytst source
chargen         19/udp          ttytst source
ftp-data        20/tcp
ftp             21/tcp
...
```

```
# service --status-all
 [ + ]  acpid
 [ + ]  apache2
 [ + ]  apparmor
 [ ? ]  apport
 [ + ]  atd
 [ + ]  chef-client
 [ ? ]  console-setup
 [ + ]  cron
 [ ? ]  cryptdisks
 [ ? ]  cryptdisks-early
 [ - ]  dbus
 [ ? ]  dns-clean
 [ + ]  friendly-recovery
 [ - ]  grub-common
 [ ? ]  irqbalance
 [ ? ]  killprocs
 [ ? ]  kmod
 [ - ]  landscape-client
 [ ? ]  mysql
 [ ? ]  networking
 [ ? ]  ondemand
 [ ? ]  open-vm-tools
 [ ? ]  pppd-dns
 [ - ]  procps
 [ + ]  puppet
 [ ? ]  rc.local
 [ + ]  resolvconf
 [ + ]  rpcbind
 [ - ]  rsync
 [ + ]  rsyslog
 [ ? ]  screen-cleanup
 [ ? ]  sendsigs
 [ + ]  ssh
 [ - ]  sudo
 [ + ]  udev
 [ ? ]  umountfs
 [ ? ]  umountnfs.sh
 [ ? ]  umountroot
 [ - ]  unattended-upgrades
 [ - ]  urandom
 [ - ]  virtualbox-guest-utils
 [ ? ]  virtualbox-guest-x11
 [ - ]  x11-common
```

```sh
$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
...
```
