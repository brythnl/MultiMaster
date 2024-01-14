## Getting Started
1. Create all containers
```bash
docker compose create
```

2. Start Salt Masters
```bash
docker compose start salt-master1 salt-master2
```

3. Copy `master_sign.pub` and `master_sign.pem` to `salt-master2`

4. Restart `salt-master2`
```bash
docker compose restart salt-master2
```

5. Start Salt Minions
```bash
docker compose start salt-minion1 salt-minion2
```

6. Copy `master_sign.pub` to Salt Minions

7. Restart Salt Minions
```bash
docker compose restart salt-minion1 salt-minion2
```

8. Accept keys in Salt Masters
```bash
salt-key -Ay
```
