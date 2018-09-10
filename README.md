# Ansible Role: network

An Ansible role that wraps the distribution/OS specific network configuration role for Debian and OpenBSD.

## Role Variables

Available common variables are listed below, along with default values (see `defaults/main.yml`):

    network_ethernet_interfaces: []                 # the list of ethernet interfaces
    network_vlan_interfaces: []                     # the list of vlan interfaces
        
The lists of the differents interfaces to configure. See distrib role for specific values.
    
For specific variables, see the distrib role.

## Dependencies

None.

## Example Playbook

None (see distrib role).
              
## Todo

Make it available for OpenBSD.

## License

```
Copyright (c) 2018 Tristan Weil <titou@lab.t18s.fr>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```
