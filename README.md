[![ansible-lint](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/lint.yml/badge.svg)](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/lint.yml)
[![molecule test](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/molecule.yml/badge.svg)](https://github.com/Rosa-Luxemburgstiftung-Berlin/rls.nextcloud-spreed-signaling/actions/workflows/molecule.yml)

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

