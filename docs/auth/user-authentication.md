# User Authentication

In the [previous example](Adding-an-SSH-target), we've reused the Warpgate's `admin` user, which only had a password as its only way to authenticate. Currently, Warpgate supports passwords, public keys or password+public key as authentication methods.

## Changing a user's password

[Log into the Warpgate admin UI](https://github.com/warp-tech/warpgate/wiki/Accessing-the-admin-UI) and navigate to `Config` > `Users` > `admin` and click `Change` next to the password credential:

![](https://user-images.githubusercontent.com/161476/189997150-7cfb9721-69e0-4083-b2a8-5c06d92f2282.png){width="500"}

## Adding a public key for a user

- Grab the user's public key in OpenSSH format (normally, you can just copy the `~/.ssh/id_<type>.pub` file contents and strip the name, leaving just `<key type> <public key bytes>`, e.g.:

```
ssh-ed25519 AAAAC...bD4I
```

- Click `Add public key` and paste it:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189997284-273478eb-634e-4cc9-8ad8-5d9d2a5f8df4.png">

## Requiring multiple authentication factors

Warpgate can require a client to present both a public key and a password.

- In the `Auth policy` > `SSH` section, uncheck `Any credential` and select both `Password` and `Key`:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189997437-8cba652c-7ff4-43f4-83fc-9ec6492ab351.png">

## Using roles to assign access

You can use _roles_ to grant a new user access to multiple targets at once (or assign multiple users to a target).

- Create and remove roles under `Config` > `Roles`.
- Assign roles to users and targets on their respective configuration pages.
