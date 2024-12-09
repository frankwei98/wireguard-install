# WireGuard installer for LXC

**This project is a bash script that aims to setup a [WireGuard](https://www.wireguard.com/) VPN on a Linux LXC container, as easily as possible!**

WireGuard is a point-to-point VPN that can be used in different ways. Here, we mean a VPN as in: the client will forward all its traffic through an encrypted tunnel to the server.
The server will apply NAT to the client's traffic so it will appear as if the client is browsing the web with the server's IP.

The script is based on [angristan/wireguard-install](https://github.com/angristan/wireguard-install/), I modify the code to run in my Proxmox LXC container.

## Requirements

### Kernel

Linux kernel have to be greater than 5.6 that have kernel support for Wireguard

You can test by `lsmod | grep wireguard`, for example in Debian 12:

```bash
root@wg-test:~# lsmod | grep wireguard
wireguard             110592  0
curve25519_x86_64      36864  1 wireguard
libchacha20poly1305    20480  1 wireguard
libcurve25519_generic    45056  2 curve25519_x86_64,wireguard
ip6_udp_tunnel         16384  1 wireguard
udp_tunnel             32768  1 wireguard
```

### Distros

Supported distributions:

- Debian >= 11 (Tested on Debian 12 container)
- Ubuntu >= 21 (Not tested)

## Usage

### Enable TUN support for container

For Proxmox VE, please refer to [https://pve.proxmox.com/wiki/OpenVPN_in_LXC](https://pve.proxmox.com/wiki/OpenVPN_in_LXC) to expose TUN into container. Wireguard will needed it to handle connections.

### Setup in container

Download and execute the script. Answer the questions asked by the script and it will take care of the rest.

```bash
curl -O https://raw.githubusercontent.com/frankwei98/wireguard-lxc-install/master/wireguard-install.sh
chmod +x wireguard-install.sh
./wireguard-install.sh
```

It will install WireGuard (kernel module and tools) on the container, configure it, create a systemd service and a client configuration file.

Run the script again to add or remove clients!

## Contributing

## Discuss changes

Please open an issue before submitting a PR if you want to discuss a change, especially if it's a big one.

### Code formatting

We use [shellcheck](https://github.com/koalaman/shellcheck) and [shfmt](https://github.com/mvdan/sh) to enforce bash styling guidelines and good practices.

## Credits & Licence

This project is based on [angristan/wireguard-install](https://github.com/angristan/wireguard-install/), and is under the [MIT Licence](https://raw.githubusercontent.com/angristan/wireguard-install/master/LICENSE)
