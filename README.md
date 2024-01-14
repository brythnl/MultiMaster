# Multi Master Redundancy System

A simple Salt system of 2 masters and 2 minions (clients) to demonstrate redundancy with the Multi Master method.
This repository contains two types of a Multi Master:
- `all_hot`: All Salt Masters run hot and any active master can be used to send commands to all Salt Minions.
- `with_failover`: If current master fails, a minion can have multiple masters and fail-over between them.
