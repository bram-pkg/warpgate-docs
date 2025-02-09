#

![](https://github.com/warp-tech/warpgate/raw/refs/heads/main/.github/readme/brand-dark.svg#only-dark){ width=300 }
![](https://github.com/warp-tech/warpgate/raw/refs/heads/main/warpgate-web/public/assets/brand.svg#only-light){ width=300 }

---

Warpgate is a smart SSH, HTTPS, MySQL and PostgreSQL bastion host for Linux that doesn't need special client apps.

- Set it up in your DMZ, add user accounts and easily assign them to specific hosts and URLs within the network.
- Warpgate will record every session for you to view (live) and replay later through a built-in admin web UI.
- Not a jump host - forwards your connections straight to the target instead.
- Native 2FA and SSO support (TOTP & OpenID Connect)
- Single binary with no dependencies.
- Written in 100% safe Rust.

## Start here

- [Getting started](getting-started/binary.md)
- [Getting started on Docker](getting-started/docker.md)
- [Adding an SSH target](targets/ssh.md)
- [Adding a HTTP target](targets/http.md)
- [Adding a MySQL target](targets/mysql.md)
- [Adding a PostgreSQL target (v0.11+)](targets/postgresql.md)
- [User authentication and roles](auth/user-authentication.md)

## Authentication

- [OTP (2 factor authentication)](auth/mfa.md)
- [Using tickets](auth/tickets.md)
- [SSO Authentication(v0.5+)](auth/sso.md)

## Other topics

- [Installing as a systemd service](install-as-systemd-service.md)
- [Chaining Warpgates together](chaining-warpgate.md)
- [Protocol support](protocol-support.md)
- [Log forwarding](log-forwarding.md)
- [Warpgate behind a reverse proxy](behind-reverse-proxy.md)
