# DHCP API

- [List reservation](#list-reservation)
- [Add reservation](#add-reservation)
- [Remove reservation](#remove-reservation)

## List reservation

---

```
/v1/?action=list-ips
```

**Example**

> [http://localhost:8080/v1/?action=list-ips](http://localhost:8080/v1/?action=list-ips):

```js
[
  {
    host: "DISP001",
    ip: "08:00:27:8B:80:A3",
    mac: "192.168.1.10",
    comment: "alice",
    sector: "primary",
    type: "static"
  }
];
```

**Command**

```sh
$ cat /etc/dhcp/dhcpd.conf
```

```sh
$ cat /var/lib/dhcp/dhcpd.leases
```

## Add reservation

---

```
/v1/?action=add-ip&comment=:comment&mac=:mac&host=:host&ip=:ip&sector=:sector
```

**Params**

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| :host    | String | Hostname    |
| :mac     | String | MAC Address |
| :ip      | String | IP Address  |
| :sector  | String | Sector      |
| :comment | String | Comment     |

**Example**

> [http://localhost:8080/v1/?action=add-ip&comment=alice&mac=08:00:27:8B:80:A3&host=DISP001&ip=192.168.1.10&sector=primary](http://localhost:8080/v1/?action=add-ip&comment=alice&mac=08:00:27:8B:80:A3&host=DISP001&ip=192.168.1.10&sector=primary):

```js
{
  "status":"host added successfully"
}
```

**Command**

```
# echo "host DISP001 {hardware ethernet 08:00:27:8B:80:A3; fixed-address 192.168.1.10;} # alice (primary)" | sudo tee --append /etc/dhcp/dhcpd.conf
# service isc-dhcp-server restart
```

```
$ cat /etc/dhcp/dhcpd.conf
```

## Remove reservation

---

```
/v1/?action=rm-ip&ip=:ip
```

**Params**

| Name | Type   | Description |
| ---- | ------ | ----------- |
| :ip  | String | IP Address  |

**Example**

> [http://localhost:8080/v1/?action=rm-ip&ip=192.168.1.10](http://localhost:8080/v1/?action=rm-ip&ip=192.168.1.10):

```js
{
  "status":"host removed successfully"
}
```

**Command**

```
# sed '/192.168.1.10/d' /etc/dhcp/dhcpd.conf
# service isc-dhcp-server restart
```

```
$ cat /etc/dhcp/dhcpd.conf
```
