openbsd-ypldap
=============

This role configures an OpenBSD machine to authenticate against an ldap server.

Requirements
------------

- OpenBSD


Role Variables
--------------

| Variable | Default Value | Description |
| -------- | ------------- | ----------- |
| `ypldap_interval` | 60 | Number of seconds `ypldap` should query `ldap_server` for user information. |
| `ldap_server` | "127.0.0.1" | Server running LDAP. | 
| `ldaps` | True | Should we connect to `ldap_server` using TLS? |
| `cafile` | undefined | Path to the CA file. By default, if no `cafile` is specified, `/etc/ssl/cert.pem` is used. | 
| `ldap_domain` | "bolddaemon" | This is the name of your domain. If your FQDN was "example.com", this value would be "example". |
| `ldap_tld` | "com" | The TLD of your domain. If your FQDN is "example.com", this would be "com". |
| `ldap_admin` | "admin" | The `rootdn`. This will ultimately resolve to: `cn={{ ldap_admin }},dc={{ ldap_domain }},dc={{ ldap_tld }}`. |
| `ldap_admin_pass` | "welcome" | Password for `rootdn`. This will be piped to `encrypt(1)` and stored in `/etc/ldapd.conf` as a hash.|

Dependencies
------------

- OpenBSD

Example Playbook
----------------

    - hosts: openbsd_ypldap_clients
      roles:
         - { role: ypldap, tags: ["clients", "ypldap"] }

License
-------

```
/*
 * Copyright (c) 2018 Aaron Bieber <aaron@bolddaemon.com>
 *
 * Permission to use, copy, modify, and distribute this software for any
 * purpose with or without fee is hereby granted, provided that the above
 * copyright notice and this permission notice appear in all copies.
 *
 * THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
 * WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
 * MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
 * ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
 * WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
 * ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
 * OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
 */
 ```
