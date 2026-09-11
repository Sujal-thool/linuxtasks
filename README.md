# DAY 1 --- Linux and AWS EC2 Network Tasks

This README documents the commands used for the five Linux and AWS EC2
networking tasks in Day 1.

## Environment

-   Cloud Platform: Amazon Web Services (AWS)
-   Service: EC2
-   Operating System: Amazon Linux
-   Network Interface: `ens5`

------------------------------------------------------------------------

# TASK 1 --- Linux IP Investigation

## Commands

``` bash
echo "IP ADDRESS"
hostname -I
```

``` bash
echo "NETWORK INTERFACE"
ip -br addr
```

``` bash
echo "DEFAULT ROUTE"
ip route
```

``` bash
echo "DNS INFORMATION"
cat /etc/resolv.conf
```

``` bash
echo "NETWORK CONFIGURATION"
ip addr
```

## Purpose

These commands are used to identify the server IP address, network
interface, default route, DNS configuration, and complete network
configuration.

------------------------------------------------------------------------

# TASK 2 --- IPv4 Address Analysis

## Commands

``` bash
echo "IPV4 ADDRESS"
hostname -I
```

``` bash
echo "IPV4 CONFIGURATION"
ip -4 addr show ens5
```

``` bash
echo "PUBLIC IP"
curl -4 ifconfig.me
```

``` bash
echo "GATEWAY CONNECTIVITY"
ping -c 4 172.31.32.1
```

``` bash
echo "DNS SERVER"
nslookup amazon.com 172.31.0.2
```

``` bash
echo "NETWORK NEIGHBORS"
ip neigh
```

## Purpose

These commands are used to analyze the IPv4 configuration, public IP
address, gateway connectivity, DNS server, and neighboring network
devices.

------------------------------------------------------------------------

# TASK 3 --- Dynamic IP Investigation

## Before Reconnect

``` bash
echo "BEFORE DISCONNECT"
hostname -I
```

``` bash
echo "NETWORK STATUS"
ip link show ens5
```

``` bash
echo "IP CONFIGURATION"
ip addr show ens5
```

## Reconnect

For a remote EC2 instance, safely reboot the server:

``` bash
echo "RECONNECT NETWORK"
sudo reboot
```

Reconnect to the EC2 instance after it becomes available.

## After Reconnect

``` bash
echo "AFTER RECONNECT"
hostname -I
```

## Purpose

The IP address before and after reconnecting is compared to investigate
whether the dynamically assigned private IP changes.

------------------------------------------------------------------------

# TASK 4 --- Cloud Linux Server & IP

## Commands

``` bash
echo "SSH CONNECTION"
whoami
```

``` bash
echo "HOSTNAME"
hostname
```

``` bash
echo "PRIVATE IP"
hostname -I
```

``` bash
echo "IP CONFIGURATION"
ip -4 addr show ens5
```

``` bash
echo "PUBLIC IP"
curl -4 ifconfig.me
```

``` bash
echo "DEFAULT GATEWAY"
ip route | grep default
```

## Purpose

These commands verify the EC2 SSH session, hostname, private IP, IP
configuration, public IP, and default gateway.

------------------------------------------------------------------------

# TASK 5 --- Cloud Network Troubleshooting

## 1. Check IP Address

``` bash
echo "IP ADDRESS"
hostname -I
```

## 2. Check Network Interface

``` bash
echo "NETWORK INTERFACE"
ip -br addr
```

## 3. Check Default Route

``` bash
echo "DEFAULT ROUTE"
ip route | grep default
```

## 4. Check Network Connectivity

``` bash
echo "NETWORK CONNECTIVITY"
ping -c 4 8.8.8.8
```

## 5. Check Nginx Service

``` bash
echo "NGINX SERVICE"
sudo systemctl status nginx
```

## 6. Check Listening Ports

``` bash
echo "LISTENING PORTS"
sudo ss -tulpn
```

## 7. Check Firewall

``` bash
echo "FIREWALL STATUS"
sudo systemctl status firewalld
```

## 8. Fix Nginx

``` bash
echo "FIX NGINX"
sudo systemctl start nginx
```

## 9. Verify Nginx

``` bash
echo "NGINX SERVICE"
sudo systemctl status nginx
```

## 10. Check Port 80

``` bash
echo "LISTENING PORT 80"
sudo ss -tulpn | grep ':80'
```

## 11. Final Service Test

``` bash
echo "FINAL SERVICE TEST"
curl http://13.236.76.244/index.html
```

## Troubleshooting Documentation

### Problem

The Nginx web service could not initially be accessed.

### Commands Used

Network configuration, connectivity, Nginx service status, listening
ports, and firewall status were checked using the commands above.

### Initial Output

Nginx was found to be inactive:

``` text
Active: inactive (dead)
```

Port 80 was also not listening.

### Cause

The Nginx service was not running.

### Solution

Nginx was started with:

``` bash
sudo systemctl start nginx
```

The Nginx configuration was subsequently corrected and the service
restarted where required.

### Final Result

Nginx became active and port 80 started listening.

A final request to the EC2 public IP returned the Nginx welcome page:

``` text
Welcome to nginx!
```

This demonstrates that the web service was successfully restored.

------------------------------------------------------------------------

# Important Notes

-   Use a normal hyphen `-` in command options, not the longer dash `–`.

-   Example:

    ``` bash
    hostname -I
    ```

    not:

    ``` bash
    hostname –I
    ```

-   Linux commands are case-sensitive. Use `whoami` and `hostname` in
    lowercase.

-   For a remote EC2 instance, avoid manually bringing the main network
    interface down unless you have another way to access the instance.
