# Home Assistant Add-on: Dnsmasq dhcp

## Installation

Follow these steps to get the add-on installed on your system:

1. Navigate in your Home Assistant frontend to **Supervisor** -> **Add-on Store**.
2. Find the "Dnsmasq dhcp" add-on and click it.
3. Click on the "INSTALL" button.

## How to use

The add-on has a couple of options available. For more detailed instructions
see below. The basic thing to get the add-on running would be:

1. Start the add-on.

## Configuration

The Dnsmasq add-on can be tweaked to your likings. This section
describes each of the add-on configuration options.

Example add-on configuration:

```yaml
dns:
  - 8.8.8.8
  - 8.8.4.4
forwards:
  - domain: mystuff.local
    server: 192.168.1.40
hosts:
  - host: home.mydomain.io
    ip: 192.168.1.10
  - host: device.mydomain.io
    mac: AA:BB:CC:DD:EE:FF
services:
  - srv: _ldap._tcp.pdc._msdcs.mydomain.io
    host: dc.mydomain.io
    port: 389
    priority: 0
    weight: 100
networks:
  - gateway: 192.168.1.1
    netmask: 255.255.255.0
    broadcast: 192.168.1.255
    range_start: 192.168.1.50
    range_end: 192.168.1.99
domain: mystuff.local
lease_time: 24h
```

### Option: `dns` (required)

Upstream DNS servers, where DNS requests that can't
be handled locally, are forwarded to. By default it is configured to have
Google's public DNS servers: `"8.8.8.8", "8.8.4.4"`.

Port can be specified using # separator, eg. `"192.168.1.2#1053"`

### Option: `forwards` (optional)

This option allows you to list domain that are forwarded to a different
(not the default) upstream DNS server.

#### Option: `forwards.domain`

The domain to forward to a different upstream DNS server.

#### Option: `forwards.server`

The DNS server to forward the request for this domain to.

### Option: `hosts` (optional)

This option allows you to provide local static answer for your DNS server.

This is helpful for making addresses resolve on your internal network and
even override external domains to be answered with a local address.

For example, one could set `myuser.duckdns.org` to resolve directly to a
internal IP address, e.g., `192.168.1.10`. While outside of this network,
it would resolve normally.

This option allows you to create a so called: Split DNS.

#### Option: `hosts.host`

The hostname or domainname to resolve locally.

#### Option: `hosts.mac` (optional)

The MAC address of the client device.

#### Option: `hosts.ip` (optional)

The IP address Dnsmasq should respond with in its DNS answer.

### Option: `services` (optional)

This option allows you to provide srv-host records.

#### Option: `services.srv`

The service to resolve.

#### Option: `services.host`

The host that contain the service.

#### Option: `services.port`

The port number for the service.

#### Option: `services.priority`

The priority for the service.

#### Option: `services.weight`

The weight for the service.

### Option: `domain` (optional)

Your network domain name, e.g., `mynetwork.local` or `home.local`

### Option: `lease_time` (optional)

The default time that the IP is leased to your client.
Defaults to `24h`, which is one day.

### Option: `networks` (optional)

This option defines settings for one or multiple networks for the DHCP server
to hand out IP addresses for.

At least one network definition in your configuration is required for the
DHCP server to work.

#### Option: `networks.subnet`

Your network schema/subnet. For example, if your IP addresses are `192.168.1.x`
the subnet becomes `192.168.1.0`.

#### Option: `networks.netmask`

Your network netmask. For example, if your IP addresses are `192.168.1.x` the
netmask becomes `255.255.255.0`.

#### Option: `networks.range_start`

Defines the start IP address for the DHCP server to lease IPs for.
Use this together with the `range_end` option to define the range of IP
addresses the DHCP server operates in.

#### Option: `networks.range_end`

Defines the end IP address for the DHCP server to lease IPs for.

#### Option: `networks.broadcast`

The broadcast address specific to the lease range. For example, if your
IP addresses are `192.168.1.x`, the broadcast address is usually `192.168.1.255`.

#### Option: `networks.gateway`

Sets the gateway address for that the DHCP server hands out to its clients.
This is usually the IP address of your router.

#### Option: `networks.interface` (optional)

The network interface to listen to for this network, e.g., `eth0`.

## Support

Got questions?

You have several options to get them answered:

- The [Home Assistant Discord Chat Server][discord].
- The Home Assistant [Community Forum][forum].
- Join the [Reddit subreddit][reddit] in [/r/homeassistant][reddit]

In case you've found a bug, please [open an issue on our GitHub][issue].

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/dotpao/hassio-addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/dotpao/hassio-addons/repository
