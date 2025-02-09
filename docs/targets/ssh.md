# Adding an SSH target

This page explains the process of adding a new SSH target host to Warpgate and allowing users to connect to it.

## Authentication setup

### Preferred: public-key auth

Warpgate has its own set of SSH keys which the target host must trust in order for connections to work.

You can view these keys on the _SSH_ page of the Admin UI, or via the `warpgate client-keys` CLI command:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/177407816-4b055316-6a46-476b-8ad7-e00cbb173dec.png">


```
$ warpgate client-keys
13:59:41  INFO Using config: "/etc/warpgate.yaml" (users: 1, targets: 2, roles: 1)
Warpgate SSH client keys:
(add these to your target's authorized_keys file)

ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINt47WEjoLc62RyZkSD5IDkyLjdgq2Kbq+UaM+3RBsT5
rsa-sha2-256 AAAADHJzYS[...]
```

The keys are listed in the order of preference. Copy one of them and paste it at the end of the `~/.ssh/authorized_keys` file on the other side (each target host OS' user has their own `authorized_keys` file and you will need to create it if it doesn't exist yet).

### Alternative: password authentication

Although not recommended, you can use a password to authenticate against a target instead.

> _Isn't storing plaintext passwords unsafe_? 
> 
> It's not as long as the config file itself is secure. Warpgate automatically locks down the config file permissions to the bare minimum required.

## Connection setup

[Log into the Warpgate admin UI](https://github.com/warp-tech/warpgate/wiki/Accessing-the-admin-UI) and navigate to `Config` > `Targets` > `Add target` and give the new target a name:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189963201-e1acde8a-33e9-48d7-b9b2-691f961f23e1.png">

Fill out the connection and authentication info and click `Update configuration`, for example:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189963475-2a4f2a4c-a2ce-4525-abe9-57acc23940d6.png">

The target should show up on the Warpgate homepage for users that are allowed to access it: 

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189963668-da83da12-c128-4e81-b44b-4e1b6f3a9175.png">

Users will be able to click the entry to obtain connection instructions:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189963704-7d5796e8-4152-47db-bd62-2017e8bfef0d.png">

## Client setup

Now, fire up your favorite SSH client and try connecting to Warpgate:

* Host: the Warpgate host
* Port: the Warpgate SSH port (default: 2222)
* Username: `admin:<target-name>`, in this example: `admin:vm1`
* Password: your Warpgate admin password

When connecting for the first time, Warpgate will ask you to check and confirm the target host's SSH host key fingerprint (which you really should do).

Here's what it looks like with OpenSSH:

```
$ ssh admin:vm1@192.168.77.253 -p 2222
admin:vm1@192.168.77.253's password: 

 Warpgate  Selected target: vm1
 Warpgate  Host key (ssh-ed25519): AAAAC3[...]
 Warpgate  There is no trusted ssh-ed25519 key for this host.
 Warpgate  Trust this key? (y/n)

 ✓ Warpgate connected   
                        
 root ~   $       
```

From this point on, you can use this as a normal SSH connection, including SFTP etc.

While your SSH session is running, you'll be able to see its status in the Admin UI: 

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189964736-37ff8ad7-0914-49e5-b6ad-294842523a19.png">

Click the shell session entry in the _Recordings_ section for a live view and replay of the terminal session:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/177408609-8fd3dbe9-f5b2-4c16-9599-1e57d07fb03f.png">

## Up next

* [[User authentication and roles]]