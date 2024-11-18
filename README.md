[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border.json)](https://github.com/copier-org/copier)
[![Podman Badge](https://img.shields.io/badge/Podman-892CA0?logo=podman&logoColor=white)](https://podman.io/)
[![Hatch project](https://img.shields.io/badge/%F0%9F%A5%9A-Hatch-4051b5.svg)](https://github.com/pypa/hatch)
![CI](https://github.com/ansible-selfhosted/selfhosted.services.pihole/actions/workflows/ci.yml/badge.svg)
[![Ansible](https://img.shields.io/badge/Ansible-Molecule-EE0000?style=plastic&logo=ansible&logoColor=white)](https://github.com/ansible/molecule)

<!-- BEGIN_ANSIBLE_DOCS -->

# Ansible Role: [pihole](https://docs.pi-hole.net/)

A role to deploy Pi-hole using rootless Podman with systemd

## Role Requirements

- none

*Refer to services collection for general requirements*

## Role Arguments

|Option|Description|Type|Required|Default|choices|
|---|---|---|---|---|---|
|pihole_config_path|The path for the Pi-hole config.|str|False|~/.config/pihole|
|pihole_dhcp_ipv6|Enable DHCP server IPv6 support (SLAAC + RA).|bool|False|False|
|pihole_dhcp_active|Enable DHCP server.<br>Static DHCP leases can be configured with a custom `/etc/dnsmasq.d/04-pihole-static-dhcp.conf`|bool|False|False|
|pihole_dhcp_end|End of the range of IP addresses to hand out by the DHCP server (mandatory if DHCP server is enabled).|str|False|None|
|pihole_dhcp_lease_time|DHCP lease time in hours.|int|False|24|
|pihole_dhcp_port|The default port for the DHCP server.<br>Only used if DHCP server is enabled.<br>Set to 1067 for rootless mode|int|False|1067|
|pihole_dhcp_rapid_commit|Enable DHCPv4 rapid commit (fast address assignment).|bool|False|False|
|pihole_dhcp_router|Router (gateway) IP address sent by the DHCP server (mandatory if DHCP server is enabled).|str|False|None|
|pihole_dhcp_start|Start of the range of IP addresses to hand out by the DHCP server (mandatory if DHCP server is enabled).|str|False|None|
|pihole_dns|IPs delimited by `;`<br>Upstream DNS server(s) for Pi-hole to forward queries to, separated by a semicolon<br>(supports non-standard ports with `#[port number]`) e.g `127.0.0.1#5053;8.8.8.8;8.8.4.4`<br>(supports [Docker service names and links](https://docs.docker.com/compose/networking/) instead of IPs) e.g `upstream0;upstream1` where `upstream0` and `upstream1` are the service names of or links to docker services<br>Note: The existence of this environment variable assumes this as the _sole_ management of upstream DNS. Upstream DNS added via the web interface will be overwritten on container restart/recreation|str|False|8.8.8.8;8.8.4.4|
|pihole_dnsmasq_path|The path for the dnsmasq config.|str|False|~/.local/share/containers/storage/pihole|
|pihole_dnssec|Enable DNSSEC support|bool|False|False|
|pihole_dns_bogus_priv|Never forward reverse lookups for private ranges|bool|False|True|
|pihole_dns_fqdn_required|Never forward non-FQDNs|bool|False|True|
|pihole_dns_port|The default port for the DNS server.<br>Set to 1053 for rootless mode.|int|False|1053|
|pihole_domain|Domain name sent by the DHCP server.|str|False|lan|
|pihole_ipv6|For unraid compatibility, strips out all the IPv6 configuration from DNS/Web services when false.|bool|False|True|
|pihole_query_logging|Enable query logging or not.|bool|False|True|
|pihole_rev_server|Enable DNS conditional forwarding for device name resolution|bool|False|False|
|pihole_rev_server_cidr|Reverse DNS<br>If conditional forwarding is enabled, set the reverse DNS zone (e.g. `192.168.0.0/24`)|str|False|None|
|pihole_rev_server_domain|If conditional forwarding is enabled, set the domain of the local network router|str|False|None|
|pihole_rev_server_target|Router's IP<br>If conditional forwarding is enabled, set the IP of the local network router|str|False|None|
|pihole_temperature_unit|Set preferred temperature unit to `c`: Celsius, `k`: Kelvin, or `f` Fahrenheit units.|str|False|c|<li>c</li><br><li>K</li><br><li>f</li>
|pihole_timezone|Timezone for Pi-hole.|str|False|Etc/UTC|
|pihole_virtual_host|What your web server 'virtual host' is, accessing admin through this Hostname/IP allows you to make changes to the whitelist / blacklists in addition to the default 'http://pi.hole/admin/' address|str|False|<hostname>|
|pihole_web_password_file|Set an Admin password using [Docker secrets](https://docs.docker.com/engine/swarm/secrets/). If `WEBPASSWORD` is set, `WEBPASSWORD_FILE` is ignored. If `WEBPASSWORD` is empty, and `WEBPASSWORD_FILE` is set to a valid readable file path, then `WEBPASSWORD` will be set to the contents of `WEBPASSWORD_FILE`.|str|False|None|
|pihole_web_port|The default port for Pi-Hole web server.|int|False|8080|
|pihole_web_theme|User interface theme to use.|str|False|default-light|<li>default-dark</li><br><li>default-darker</li><br><li>default-light</li><br><li>default-auto</li><br><li>high-contrast</li><br><li>high-contrast-dark</li><br><li>lcars</li>
|pihole_webui_boxed_layout|Use boxed layout (helpful when working on large screens)|str|False|boxed|<li>boxed</li><br><li>traditional</li>


## Example Playbook

```
- hosts: all
  tasks:
    - name: Importing pihole role
      ansible.builtin.import_role:
        name: selfhosted.services.pihole
      vars:
```

## License

This project is licensed under the [MIT License](LICENSE)


⊂(▀¯▀⊂)

<!-- END_ANSIBLE_DOCS -->
