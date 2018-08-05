# ivansible.lin-shadowsocks-obfs
This role installs [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev#install-from-repository) server and [simple-obfs](https://github.com/shadowsocks/simple-obfs#intro) on linux

The _shadowsocks-libev_ [PPA](https://launchpad.net/~max-c-lv/+archive/ubuntu/shadowsocks-libev) currently lacks _bionic_ packages. As a workaround, _xenial_ packages are installed.

Please refer to [this Dockerfile](https://hub.docker.com/r/hongkongkiwi/shadowsocks-with-simple-obfs/) and [this Wiki](https://github.com/fconn/ss2ch/wiki/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0-%D0%BD%D0%B0-%D0%B1%D0%B0%D0%B7%D0%B5-Ubuntu-16.04) for instructions on installing _shadowsocks-libev_ and building _simple-obfs_.


## Requirements

None


## Variables

Available variables are listed below, along with default values.

    lin_ss_configs: []

    lin_ss_defaults:
      name: config
      bindip: "0.0.0.0"
      port: 443
      local_port: 1080
      password: secret
      timeout: 60
      method: aes-128-cfb

    obfs_build_deps: autoconf automake libtool asciidoc xmlto
                     libssl-dev libpcre3-dev libc-ares-dev libev-dev


## Tags

- `lin_ss_install` -- install shadowsocks-libev from PPA
- `lin_ss_obfs` -- build and install simple-obfs
- `lin_ss_services` -- configure and activate shadowsocks services


## Dependencies

None


## Example Playbook

    - hosts: vagrant-boxes
      roles:
         - role: ivansible.lin-shadowsocks-obfs
           lin_ss_configs:
             - port: 12081
               password: secret1


## License

MIT

## Author Information

Created in 2018 by [IvanSible](https://github.com/ivansible)
