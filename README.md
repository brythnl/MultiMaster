# Multi Master Redundancy System

A simple Salt system of 2 masters and 2 minions (clients) to demonstrate redundancy with the Multi Master method.

## Getting Started
1. Create all containers
```bash
docker compose create
```

2. Start salt-master1 and salt-master2 services first, to prep redundant master (salt-master2)
```bash
docker compose start salt-master1 salt-master2
```

3. Copy over PKI key pair (`master.pub` & `master.pem`) from salt-master1 over to salt-master2.
Yes, overwrite the existing key pair in salt-master2. They are located in: `/etc/salt/pki/master/`
Run `./master1-shell.sh` / `./master2-shell.sh` to open interactive shell in each master container.

4. Restart salt-master2 / redundant master
```bash
docker compose restart salt-master2
```

5. Add new (redundant) master to the minions' configuration in `/etc/salt/minion`
Run `./minion1-shell.sh` / `./minion2-shell.sh` to open interactive shell in each minion container.
```
master:
  - salt-master1
  - salt-master2 # New master
```

6. Restart minions
```bash
docker compose restart salt-minion1 salt-minion2
```

7. Accept minion keys on salt-master1 and salt-master2
```bash
salt-key -Ay
```

8. Test ping to all minions from each master
```bash
salt '*' test.ping
```
