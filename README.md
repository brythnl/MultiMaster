# What is Salt?
=> a Python-based open-source remote execution framework used for:
- Configuration management
- Automation
- Provisioning
- Orchestration

# Salt system architecture
- Master-Client Model / Publisher-Subscriber Model
    1. Master issues commands to client, client executes
    / Master publishes jobs to be executed, client subscribes to job, when job applies to client, client executes job
    2. When client finished executing job, client sends job return data back to master

    - Salt Master => Server running `salt-master` service
    - Salt Minion => Server running `salt-minion` service (registered to a particular Salt Master)

- Targets => A group of minions across one or many masters, that a job's Salt command applies to
    - e.g. `'*'` in:
     ```
     salt -v '*' pkg.install vim
     ```

- Grains => Interface to derive information about underlying system (OS, domain name, IP address, kernel, etc.)

- Salt states => declares which state a minion should be in. Makes Configuration Management possible.

# Getting Started
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
