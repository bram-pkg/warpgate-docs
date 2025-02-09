# Adding a PostgreSQL target

> This feature is available in v0.11+

This page explains the process of adding a new PostgreSQL target host to Warpgate and allowing users to connect to it.

# Authentication setup

Currently, Warpgate can connect to PostgreSQL servers with a username/password using `md5` and `password` (plaintext) auth mode.

As a PostgreSQL protocol server, Warpgate only allows secure (TLS) connections and uses `password` auth mode.

# Enabling PostgreSQL listener

Enable the PostgreSQL protocol in your config file (default: `/etc/warpgate.yaml`) if you didn't do so during the initial setup:

```diff
+ postgres:
+   enable: true
+   certificate: /var/lib/warpgate/tls.certificate.pem
+   key: /var/lib/warpgate/tls.key.pem
```

You can reuse the same certificate and key that are used for the HTTP listener.

# Connection setup

[Log into the Warpgate admin UI](https://github.com/warp-tech/warpgate/wiki/Accessing-the-admin-UI) and navigate to `Config` > `Targets` > `Add target` and give the new PostgreSQL target a name:

<img width="886" alt="Screenshot 2024-10-08 at 20 48 09" src="https://github.com/user-attachments/assets/216dc8e7-0b26-4ced-837a-75d3b0ca08bd">

Fill out the configuration:

<img width="768" alt="Screenshot 2024-10-08 at 20 48 54" src="https://github.com/user-attachments/assets/0201e348-06cc-416a-baf6-a8cfbe7620f0">

The target should show up on the Warpgate's homepage:

<img width="686" alt="Screenshot 2024-10-08 at 20 51 01" src="https://github.com/user-attachments/assets/e80d280a-e4a9-49ca-8c50-5cbad81d536d">

Users will be able to click the entry to obtain connection instructions:

<img width="711" alt="Screenshot 2024-10-08 at 20 51 16" src="https://github.com/user-attachments/assets/59c8aad3-dedc-4596-af69-94b4c4bc7abf">

# Client setup

You can now use any PostgreSQL client applications to connect through Warpgate with the following settings:

* Host: the Warpgate host
* Port: the Warpgate PostgreSQL port (default: 55432)
* Username: `admin#<target-name>` or `admin:<target-name>`, in this example: `admin#db1`
* Password: your Warpgate admin password
* TLS: enabled
* Cleartext password authentication: allowed

If your client uses a database URL, use: `postgresql://<username>#<target>:<password>@<warpgate host>:<warpgate postgresql port>?sslmode=require`

While your PostgreSQL session is running, you'll be able to see its status in the Admin UI, including the query log: 

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/179948103-7d7f84f7-68a0-40c3-be1c-60892a7f0ace.png">


# Up next

* [[User authentication and roles]]