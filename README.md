# DUID Generator

When configuring static IPv6 address reservations with DHCPv6, it often doesn't work out of the box.

Unlike DHCPv4, DHCPv6 does not directly use the client's MAC address. Instead, it relies on a different identifier known as the DUID (DHCP Unique Identifier). There are four types of DUIDs, but only two of them incorporate the client's MAC address:

* **Type 1 (DUID-LLT)**: Derived from the MAC address and a timestamp.
* **Type 3 (DUID-LL)**: Derived solely from the MAC address.

To successfully use static IPv6 address reservations with DHCPv6, you have two options:

1. Reserve the address for your DUID directly, or
2. Reserve the address for your MAC address and configure your DHCP client to use either a DUID-LL or DUID-LLT derived from that MAC address.

The second option is commonly used with the routers I work with. If you're using `dhcpcd` on `Ubuntu`, you can set your new DUID by placing it in `/var/lib/dhcpcd/duid` and then restarting `dhcpcd` and NetworkManager:

```bash
sudo systemctl restart dhcpcd
sudo systemctl restart NetworkManager
```

This repository provides functions to generate these DUIDs, along with a simple usage example. The implementation was inspired by [this discussion] with the `dhcpcd` maintainers.

## References

* [RFC 3315]

[RFC 3315]: https://datatracker.ietf.org/doc/html/rfc3315
[this discussion]: https://github.com/NetworkConfiguration/dhcpcd/issues/354
