# HTTP targets on separate domains

> This feature is available in v0.5+

Instead of using `?warpgate-target=` in the URL, you can use multiple domains/hostnames and link each to a specific target.

Accessing Warpgate over HTTP on a specific domain will then automatically select the corresponding target.

For optimal results, you want to host Warpgate on a common higher-level domain (e.g. `wg.acme.inc`, as set by the `external_host` config option), with target-specific domains as subdomains of this one (e.g. `gitlab.wg.acme.inc`) - this will prevent users from having to log in again when switching between domains (Warpgate will set its session cookie for all subdomains).

## Linking a target to a domain

Set the `http.external_host` property on the target config:

```diff
  - name: gitlab
    allow_roles:
      - "warpgate:admin"
      - qa
    http:
      url: http://10.0.0.2
+     external_host: gitlab.wg.acme.inc
```
