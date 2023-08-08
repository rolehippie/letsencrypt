# letsencrypt

[![Source Code](https://img.shields.io/badge/github-source%20code-blue?logo=github&amp;logoColor=white)](https://github.com/rolehippie/letsencrypt)
[![General Workflow](https://github.com/rolehippie/letsencrypt/actions/workflows/general.yml/badge.svg)](https://github.com/rolehippie/letsencrypt/actions/workflows/general.yml)
[![Readme Workflow](https://github.com/rolehippie/letsencrypt/actions/workflows/docs.yml/badge.svg)](https://github.com/rolehippie/letsencrypt/actions/workflows/docs.yml)
[![Galaxy Workflow](https://github.com/rolehippie/letsencrypt/actions/workflows/galaxy.yml/badge.svg)](https://github.com/rolehippie/letsencrypt/actions/workflows/galaxy.yml)
[![License: Apache-2.0](https://img.shields.io/github/license/rolehippie/letsencrypt)](https://github.com/rolehippie/letsencrypt/blob/master/LICENSE)
[![Ansible Role](https://img.shields.io/badge/role-rolehippie.letsencrypt-blue)](https://galaxy.ansible.com/rolehippie/letsencrypt)

Ansible role to fetch and publish Let&#39;s Encrypt certificates.

## Sponsor

Building and improving this Ansible role have been sponsored by my current and previous employers like **[Cloudpunks GmbH](https://cloudpunks.de)** and **[Proact Deutschland GmbH](https://www.proact.eu)**.

## Table of content

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [letsencrypt_account_email](#letsencrypt_account_email)
  - [letsencrypt_account_key](#letsencrypt_account_key)
  - [letsencrypt_cert_city](#letsencrypt_cert_city)
  - [letsencrypt_cert_country](#letsencrypt_cert_country)
  - [letsencrypt_cert_organization](#letsencrypt_cert_organization)
  - [letsencrypt_cert_paths](#letsencrypt_cert_paths)
  - [letsencrypt_cert_province](#letsencrypt_cert_province)
  - [letsencrypt_certificates](#letsencrypt_certificates)
  - [letsencrypt_challenge_mapping](#letsencrypt_challenge_mapping)
  - [letsencrypt_cluster_enabled](#letsencrypt_cluster_enabled)
  - [letsencrypt_cluster_nodes](#letsencrypt_cluster_nodes)
  - [letsencrypt_extra_certs](#letsencrypt_extra_certs)
  - [letsencrypt_nsupdate_algorithm](#letsencrypt_nsupdate_algorithm)
  - [letsencrypt_nsupdate_name](#letsencrypt_nsupdate_name)
  - [letsencrypt_nsupdate_secret](#letsencrypt_nsupdate_secret)
  - [letsencrypt_nsupdate_server](#letsencrypt_nsupdate_server)
  - [letsencrypt_production_armed](#letsencrypt_production_armed)
  - [letsencrypt_reload_services](#letsencrypt_reload_services)
  - [letsencrypt_request_output](#letsencrypt_request_output)
  - [letsencrypt_restart_services](#letsencrypt_restart_services)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.10`


## Default Variables

### letsencrypt_account_email

Email address used for Let's Encrypt

#### Default value

```YAML
letsencrypt_account_email: hostmaster@localhost
```

### letsencrypt_account_key

Path to Let's Encrypt account key

#### Default value

```YAML
letsencrypt_account_key: account.key
```

### letsencrypt_cert_city

City used for the SSL configuration

#### Default value

```YAML
letsencrypt_cert_city: Nuremberg
```

### letsencrypt_cert_country

Country used for the SSL configuration

#### Default value

```YAML
letsencrypt_cert_country: DE
```

### letsencrypt_cert_organization

Organization used for the SSL configuration

#### Default value

```YAML
letsencrypt_cert_organization: DevOps Team
```

### letsencrypt_cert_paths

Paths to store the certificates

#### Default value

```YAML
letsencrypt_cert_paths:
  - /etc/ssl/letsencrypt
```

#### Example usage

```YAML
letsencrypt_cert_paths:
  - /etc/haproxy/ssl
  - path: /etc/caddy
    owner: caddy
    group: caddy
    mode: u=rwx,g=x,o=x
```

### letsencrypt_cert_province

Province used for the SSL configuration

#### Default value

```YAML
letsencrypt_cert_province: Bavaria
```

### letsencrypt_certificates

List of certificate definitions

#### Default value

```YAML
letsencrypt_certificates: []
```

#### Example usage

```YAML
letsencrypt_certificates:
  - name: foobar
    challenge: nsupdate
    common_name: foobar.com
    alternate_names:
      - '*.foobar.com'
  - name: example
    challenge: http
    common_name: example.com
    alternate_names:
      - sub1.example.com
      - sub2.example.com
      - sub3.example.com
```

### letsencrypt_challenge_mapping

Mapping of challenge types

#### Default value

```YAML
letsencrypt_challenge_mapping:
  http: http-01
  nsupdate: dns-01
```

### letsencrypt_cluster_enabled

Enable clustered mode

#### Default value

```YAML
letsencrypt_cluster_enabled: false
```

### letsencrypt_cluster_nodes

List of nodes part of the cluster

#### Default value

```YAML
letsencrypt_cluster_nodes: []
```

#### Example usage

```YAML
letsencrypt_cluster_nodes:
  - node01
  - node02
  - node03
```

### letsencrypt_extra_certs

Additional certificates to add

#### Default value

```YAML
letsencrypt_extra_certs: []
```

#### Example usage

```YAML
letsencrypt_extra_certs:
  - foobar.pem
  - name: general.pem
    owner: root
    group: haproxy
    mode: u=rwx,g=x,o=x
```

### letsencrypt_nsupdate_algorithm

TSIG algorithm for nsupdate DNS challenges

#### Default value

```YAML
letsencrypt_nsupdate_algorithm: hmac-sha512
```

### letsencrypt_nsupdate_name

TSIG name for nsupdate DNS challenges

#### Default value

```YAML
letsencrypt_nsupdate_name:
```

### letsencrypt_nsupdate_secret

TSIG secret for nsupdate DNS challenges

#### Default value

```YAML
letsencrypt_nsupdate_secret:
```

### letsencrypt_nsupdate_server

Server used for nsupdate DNS challenges

#### Default value

```YAML
letsencrypt_nsupdate_server:
```

### letsencrypt_production_armed

Enable production authority

#### Default value

```YAML
letsencrypt_production_armed: false
```

### letsencrypt_reload_services

List of services to reload

#### Default value

```YAML
letsencrypt_reload_services: []
```

#### Example usage

```YAML
letsencrypt_reload_services:
  - haproxy
  - apache
```

### letsencrypt_request_output

Print cert information after request

#### Default value

```YAML
letsencrypt_request_output: true
```

### letsencrypt_restart_services

List of services to restart

#### Default value

```YAML
letsencrypt_restart_services: []
```

#### Example usage

```YAML
letsencrypt_restart_services:
  - traefik
```

## Discovered Tags

**_letsencrypt_**


## Dependencies

- None

## License

Apache-2.0

## Author

[Thomas Boerger](https://github.com/tboerger)
