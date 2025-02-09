# Adding a MySQL target

This page explains the process of adding a new MySQL target host to Warpgate and allowing users to connect to it.

## Authentication setup

Currently, Wargate can connect to MySQL and MariaDB servers with a username/password via the `mysql_native_password` auth mode.

As a MySQL protocol server, Warpgate only allows secure (TLS) connections and uses `mysql_clear_password` auth mode.

## Enabling MySQL listener

Enable the MySQL protocol in your config file (default: `/etc/warpgate.yaml`) if you didn't do so during the initial setup:

```diff
+ mysql:
+   enable: true
+   certificate: /var/lib/warpgate/tls.certificate.pem
+   key: /var/lib/warpgate/tls.key.pem
```

You can reuse the same certificate and key that are used for the HTTP listener.

## Connection setup

[Log into the Warpgate admin UI](https://github.com/warp-tech/warpgate/wiki/Accessing-the-admin-UI) and navigate to `Config` > `Targets` > `Add target` and give the new MySQL target a name:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189996361-ca2f0433-feae-440b-a8ae-52c6459fb913.png">

Fill out the configuration:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189996487-179ed3d1-b5b6-4ed2-b1ff-8d11579fbfaf.png">

The target should show up on the Warpgate's homepage:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189996603-aec40b1d-e876-4dee-931b-a5e09c04b2d3.png">

Users will be able to click the entry to obtain connection instructions:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189996623-2823f11f-e1f4-4d3d-9edf-312d1c6d15a6.png">

## Client setup

You can now use any MySQL/MariaDB client applications to connect through Warpgate with the following settings:

* Host: the Warpgate host
* Port: the Warpgate MySQL port (default: 33306)
* Username: `admin#<target-name>` or `admin:<target-name>`, in this example: `admin#db1`
* Password: your Warpgate admin password
* TLS: enabled
* Cleartext password authentication: allowed

If your client uses a database URL, use: `mysql://<username>#<target>:<password>@<warpgate host>:<warpgate mysql port>?sslMode=required`

While your MySQL session is running, you'll be able to see its status in the Admin UI, including the query log: 

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/179948103-7d7f84f7-68a0-40c3-be1c-60892a7f0ace.png">

## Up next

* [[User authentication and roles]]