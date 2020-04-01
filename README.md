# ivansible.srv_ss

This role installs
[shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev#install-from-repository)
server, and two protocol plugins: [v2ray](https://github.com/shadowsocks/v2ray-plugin])
and [simple-obfs](https://github.com/shadowsocks/simple-obfs#intro) (now deprecated).

The main package is installed from official Ubuntu repositories on _bionic_ or from the
_shadowsocks-libev_ [PPA](https://launchpad.net/~max-c-lv/+archive/ubuntu/shadowsocks-libev) on _xenial_.

Please refer to [this Dockerfile](https://hub.docker.com/r/hongkongkiwi/shadowsocks-with-simple-obfs/)
and [this Wiki](https://github.com/fconn/ss2ch/wiki/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0-%D0%BD%D0%B0-%D0%B1%D0%B0%D0%B7%D0%B5-Ubuntu-16.04)
for instructions on installing _shadowsocks-libev_ and building _simple-obfs_.


## Requirements

None


## Variables

Available variables are listed below, along with default values.

    srv_ss_configs: []

    srv_ss_defaults:
      name: config
      bindip: "0.0.0.0"
      port: 9443
      local_port: 1080
      password: secret
      timeout: 60
      method: aes-128-cfb

    srv_ss_obfs_build_deps:
      - autoconf
      - automake
      - libtool
      - asciidoc
      - xmlto
      - libssl-dev
      - libpcre3-dev
      - libc-ares-dev
      - libev-dev

TODO...


## Tags

- `srv_ss_install` -- install shadowsocks-libev from PPA
- `srv_ss_fix` -- aply service fixes: set `proxy` process group,
                  disable ambiend capabilities on old kernels, etc
- `srv_ss_v2ray` -- install v2ray plugin
- `srv_ss_obfs` -- build and install simple-obfs
- `srv_ss_services` -- configure and activate shadowsocks services
- `srv_ss_nginx` -- configure nginx fronting
- `srv_ss_all` -- all of above


## Dependencies

- [ivansible.lin_base](https://github.com/ivansible/lin-base)
  - common ansible handlers, default parameters and custom modules
  - handler to restart syslog service
  - global flag `lin_compress_logs` enables compression of rotated logs
- [ivansible.srv_cdn](https://github.com/ivansible/srv-cdn)
  - installs nginx and creates directory for mixin configs

## Example Playbook

    - hosts: myproxy
      roles:
         - role: ivansible.srv_ss
           srv_ss_configs:
             - port: 12081
               password: secret1


## License

MIT

## Author Information

Created in 2018-2020 by [IvanSible](https://github.com/ivansible)
