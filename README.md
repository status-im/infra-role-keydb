# Description

This role configures [KeyDB](https://docs.keydb.dev/) running in a Docker container.

* It supports single instance, replica, and multi-master topologies. 
* Auth is enforced with the default user + password (`key_db_password`) — used by both clients and replication. 
* No TLS is configured (assume private network).
* Includes host-level tuning: disables Transparent Huge Pages (THP), sets `vm.overcommit_memory=1`.

# Configuration

Depending on the chosen topology the bare minimum would be:

### Single instance
```yaml
key_db_password: 'changeMeIfYouCan'
key_db_topology: 'single'
```

### Replica
```yaml
key_db_password: 'changeMeIfYouCan'
key_db_topology: 'replica'
key_db_master_host: '10.0.0.2'
key_db_master_port: 6379
```

### Multi Master
```yaml
key_db_password: 'changeMeIfYouCan'
key_db_topology: 'multi_master'
key_db_peer_list:
- { host: '10.0.0.2', port: 6379 }
- { host: '10.0.0.3', port: 6379 }
```