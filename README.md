# Ansible Role: network

An Ansible Role that wraps the distribution/OS specific network configuration role.

*WARNING*: this role handles network reconfigurations and should not hang Ansible if used on the main interface.
However, it is recommended to reboot your host if you modify in depth your network settings. 

[![Actions Status](https://github.com/tristan-weil/ansible-role-network/workflows/molecule/badge.svg?branch=master)](https://github.com/tristan-weil/ansible-role-network/actions)

## Role Variables

Available common variables are listed below, along with default values (see `defaults/main.yml`):

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| network_dns_search | [] | a list of search domains |
| network_dns_inet_nameservers | [] | a list of IPv4 dns servers (overrides DHCP's list) |
| network_dns_inet6_nameservers | [] | a list of IPv6 dns servers (overrides DHCP's list) |
| network_dns_options | [] | a list of <*network dns option*>to add in the /etc/resolv.conf file |
| network_dhcp_send_options | {{ _network_dhcp_default_send_options }} | a list of <*dhcp option/value*> to send to the DHCP server |
| network_dhcp_request_options | {{ _network_dhcp_default_request_options }} | a list of DHCP options to request |
| network_dhcp_require_options | {{ _network_dhcp_default_require_options }} | a list of required DHCP options |
| network_dhcp_default_options | {{ _network_dhcp_default_default_options }} | a list of <*dhcp option/value*> used as default if not provided by the DHCP server |
| network_dhcp_append_options | {{ _network_dhcp_default_append_options }} | a list of <*dhcp option/value*> to append to the ones provided by the DHCP server |
| network_dhcp_prepend_options | {{ _network_dhcp_default_prepend_options }} | a list of <*dhcp option/value*> to prepend to the ones provided by the DHCP server |
| network_dhcp_supersede_options | {{ _network_dhcp_default_supersede_options }} | a list of <*dhcp option/value*> to supersede to the ones provided by the DHCP server |
| network_dhcp_ignore_options | {{ _network_dhcp_default_ignore_options }} | a list of <*dhcp option/value*> to ignore if sent by the DHCP server |
| network_dhcp_options_definitions | {{ _network_dhcp_default_options_definitions }} | a list of DHCP options' definitions |
| network_ethernet_interfaces | [] | a list of <*ethernet interface*> |
| network_vlan_interfaces | [] | a list of <*vlan interface*> |

### <*dhcp option/value*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| option        | the resolv.conf option's name |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| value        | | the value of the option |

### <*dhcp option/value*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| option        | the DHCP option's name |
| value         | the value |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

### <*ethernet interface*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| device        | the device's name |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| options       | []      | a list of <*device's option*> |
| inet          |         | a dictionnary used to configure <*INET*> (IPv4) |
| inet6          |         | a dictionnary used to configure <*INET6*> (IPv6) |

### <*vlan interface*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| device        | the device's name |
| parent        | the name of the parent's device |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| options       | []      | a list of <*device's option*> |
| inet          |         | a dictionnary used to configure <*INET*> (IPv4) |

#### <*device option*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| hwaddress     |         | a MAC address |
| mtu           |         | a MTU |

#### <*INET*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| type          | *static / dhcp*: to configure the device with a static address or DHCP |

Mandatory variables with type **static**:

| Variable      | Description |
| :------------ | :---------- |
| address       | the IPv4 address |
| prefixlen     | the prefixlen |
| netmask       | the netmask (dotted form) if the **prefixlen** is not defined |
| broadcast     | the broadcast address |
| gateway       |  the gateway address |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| commands      | []      | a list of commands to launch after the configuration of the device |

#### <*INET6*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| type          | *static / auto / dhcp*: to configure the device |

Mandatory variables with type **static**:

| Variable      | Description |
| :------------ | :---------- |
| address       | the IPv4 address |
| prefixlen     | the prefixlen |
| netmask       | the netmask (dotted form) if the **prefixlen** is not defined |
| broadcast     | the broadcast address |
| gateway       |  the gateway address |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| commands      | []      | a list of commands to launch after the configuration of the device |

Optional variables with type **auto**:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| autoconf      |         | a dictionary <*INET6 Autoconf*> to configure autoconf options|
| ra            | on      | *off / on / forwarding*: allow to listen (and forward) the Route Advertisments |
| dhcp          |         | a dictionary <*INET6 DHCP*> to configure DHCPv6 |

Optional variables with type **dhcp**:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| dhcp          |         | a dictionary <*INET6 DHCP*> to configure DHCPv6 |

#### <*INET6 Autoconf*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| privacy       | prefer | *off / assign / prefer*: enable the privacy extension |

#### <*INET6 DHCP*>

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| enabled       | False | *True / False*: to enable stateless configuration (with type **auto**) |
| prefix_delegation | False | *True / False*: to enable prefix delegation's requests |

## Dependencies

- ansible-role-network
- ansible-role-linux_kernel_module

## Example Playbook

    - hosts: 'debian'
      tasks:
        - import_role:
            name: 'network'
          vars:
            network_dns_inet_nameservers:
              - 9.9.9.9
    
            network_dns_inet6_nameservers:
              - 2606:4700:4700::1111
    
            network_ethernet_interfaces:
              - device: eth0
                options:
                  mtu: 1492
    
                inet:
                  type: static
    
                  address: 10.0.2.15
                  netmask: 255.255.0.0
                  broadcast: 10.0.2.255
                  gateway: 10.0.2.2
    
                inet6:
                  type: static
    
                  address: fe80::9656:d028:8652:66b6
                  prefixlen: 64

## Todo

Add aliases.

## Dependencies

See [requirements_galaxy.yml](https://github.com/tristan-weil/ansible-role-network/blob/master/requirements_galaxy.yml)

## Supported platforms

See [meta/main.yml](https://github.com/tristan-weil/ansible-role-network/blob/master/meta/main.yml)

## License

See [LICENSE.md](https://github.com/tristan-weil/ansible-role-network/blob/master/LICENSE.md)
