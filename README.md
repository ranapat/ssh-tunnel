# ssh tunnel

Handle ssh tunnel with another machine.

Can establish, reset, stop, test and generate ssh configuration.

## What is this

Do you have a machine without a real IP or behind a firewall?
Do you have a spare machine with real IP?
Do you want to access the first one somehow from outside?

SSH tunnel is just a simple wrap around what ssh provides by default.

## Basic idea

Machine A is unreachable.

Machibe B is reachable.

- A links to B with ssh tunnel.

- From outside you link B.

- From B you enter A as the tunnel is open.

## How to enter A from B

```
ssh <user>@localhost -p <port>
```

Or if you use .ssh/config like this:

```
Host your_host
    Port your_port
    User your_user
    HostName localhost
```

just try:

```
ssh your_host
```

You can generate this config automatically from A and copy it to B with
```
ssh_tunnel register
```

## Port mapping

If machine B (the public one) has port mapping you can directly

ssh <user on A>@<host or ip of B> -p <port that you exposed>

## Basic usage

### Handing configuration

- If you do not want to make configuration and just to use it open ssh_tunnel and change the defailt values of the variables.
- If you want you can configure with
```
ssh_tunnel config
```

### Just make sure it's executable before you run it

```
chmod +x ssh_tunnel
```

### Show help

To get the usage summary

```
ssh_tunnel
```

### Config

To make it easier to work you will be asked on every run to provide config.
You can get help to generate it with :

```
ssh_tunnel config
```

The structure will be like this
```
remote_host=<public machine host/ip>
remote_port=<public machine port>
local_port=<your local machine port>
local_name=<name for the config when you generate it with register>
local_user=<your local username>
```

### Start

Start will also check if it's already running and if it's running is it still active.

```
ssh_tunnel start
```

### Restart

Kills the current instance and starts a new one

```
ssh_tunnel restart
```

### Stop

Will check if it's running and stop it

```
ssh_tunnel stop
```

### Status

Checks for the status of the connection

```
ssh_tunnel status
```

### Register

If you want to generate a new .ssh config on the host server you can do it.
The result will be a normal ssh_config record in a folder inside ${HOME}/.ssh/.ssh.d/<name>
If you do not have rights to write there it will failt with some errors.

If your sshd version does not support .ssh/.ssh.d folder structure link it manually or call the ssh.d/<name> on ssh or copy it in the general file.

```
ssh_tunnel register
```
