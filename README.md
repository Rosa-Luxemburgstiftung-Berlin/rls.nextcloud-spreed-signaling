[![ansible-lint](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/lint.yml/badge.svg)](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/lint.yml)
[![molecule test](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/molecule.yml/badge.svg)](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/molecule.yml)
[![Ansible 12 read](https://img.shields.io/badge/ansible_12-ready-green?logo=ansible&labelColor=black)](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/molecule-ansible12.yml)

# rls.nextcloud-spreed-signaling
ansible role to setup a standalone nextcloud-spreed-signaling server :  https://github.com/strukturag/nextcloud-spreed-signaling

it supports instaling the nextcloud-spreed-signaling server from:
  * debian (backports)
  * build from src
  * struktur ag repo (requires a subscription key)

## debian package from backports

```yaml
- name: install deb from backports
  hosts: talk
  vars:
    nextcloud_hostname: cloud.next.invalid.com
    spreed_secret: Al4iem0s
  roles:
    - rls.nextcloud-spreed-signaling
```

## build from src

requires role [gantsign.golang](https://github.com/gantsign/ansible-role-golang)

```yaml
- name: install
  hosts: talk
  vars:
    nextcloud_hostname: cloud.next.invalid.com
    spreed_secret: Al4iem0s
    struktur_spreed_from_source: true
    struktur_spreed_build_version: v2.0.2
    golang_version: '1.23.5'
    golang_install_dir: /opt/go
  roles:
    - gantsign.golang
    - rls.nextcloud-spreed-signaling
```

### update from src
if you like to update a existing installation from source, run:
```
ansible-playbook -e struktur_spreed_build_update=true -e struktur_spreed_build_version=v2.0.3 ...
```


## debian package from struktur ag repo

requires a subscription key

```yaml
- name: install
  hosts: talk
  vars:
    nextcloud_hostname: cloud.next.invalid.com
    spreed_secret: Al4iem0s
    struktur_spreed_customerid: ABC123xyz890
  roles:
    - rls.nextcloud-spreed-signaling
```

## use tls/ssl

define the vars:

  * `spreed_cert_pem`
  * `spreed_cert_key`
  * `janus_cert_pem`
  * `janus_cert_key`
