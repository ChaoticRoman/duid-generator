# DUID Generator

If we want to use static IPv6 address reservation with DHCPv6,
it is usually not working out of the box. Static reservation
in DHCPv6 does not use directly a MAC address of the client.
Instead, DHCPv6 relies on a different identifier called the DUID
(DHCP Unique Identifier). There are four types of DUID and
only two of them, Type 1 (DUID-LLT, derived from MAC address
and time) and Type 3 (DUID-LL, derived from MAC address only).

To be able to use static IPv6 address reservation with DHCPv6,
you should either

1. reserve it for your DUID directly, or
2. reserve it for your MAC address and DUID-LL or DUID-LLT
    derived from that MAC address.

The second choice is popular with routers I work with. If you
use `dhcpcd` and `Ubuntu`, put your new DUID
to `/var/lib/dhcpcd/duid` and restart `dhcpcd` and NetworkManager:

```
sudo systemctl restart dhcpcd
sudo systemctl restart NetworkManager
```

Here are functions provided functions to generate these with
simple usage example. Inspired by [this discussion] with
`dhcpcd` maintainers.

## Reference:

* [RFC 3315]

[RFC 3315]: https://datatracker.ietf.org/doc/html/rfc3315
[this discussion]: https://github.com/NetworkConfiguration/dhcpcd/issues/354
