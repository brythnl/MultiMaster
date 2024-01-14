# Multi Master Redundancy System

A simple Salt system of 2 masters and 2 minions (clients) to demonstrate redundancy with the Multi Master method.
This repository contains two types of a Multi Master:
- `all_hot`: All Salt Masters run hot and any active master can be used to send commands to all Salt Minions.

![image](https://github.com/brythnl/MultiMaster/assets/98424627/224c40d0-ce78-42da-9d5f-ec53b1fb15b0)

- `with_failover`: If current master fails, a minion can have multiple masters and fail-over between them.

![image](https://github.com/brythnl/MultiMaster/assets/98424627/a85f45ca-58fd-4aea-86a3-186c9bac4532)

