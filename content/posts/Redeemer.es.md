+++
date = 2024-07-04
title = "HTB Redeemer WriteUp"
slug = ""
author = ["R4NC0X"]
description = "HackThebox 'Redeemer' WriteUp"
draft = false
tags = [
    "HTB",
    "Maquina",
    "Linux",
    "Redis",
    "Evaluacion de vilnerabilidad",
    "Base de datos",
    "Reconocimiento",
    "Acceso anonimo/invitado",
]
+++

# Redeemer -- HacktheBox

- Sistema: _Linux_
- Dificultad: _Muy Facil_
- Plataforma: _HacktheBox_

!['Redeemer' Avatar](/images/Redeemer/Redeemer.webp)

___

## Resumen 

"Redeemer" es una maquina de dificultad "Muy Facil" de la plataforma `HackTheBox`. Redeemer forma parte de los laboratorios de `Punto de Partida`.

Para completar esta maquina utilize nmap para realizar escaneo de puertos a la dirrecion ip `10.129.5.10`, La maquina propone el uso del servicio `Redis` cuyo protocolo es el `6379` ya confirmado que el puerto esta abierto procedi a usar el comando `redis-cli -h [DireccionIp]`, con esto ingrese a la maquina y usando el comando `INFO` pude analizar que version de redis esta funcionando asi como saber cuantos clientes y keys hay, teniendo toda esta informacion con el uso del comando `KEYS *` listo las keys que tiene la maquina, una de las 4 lleva el nombre de `flag` por lo que con el comando `GET flag` listo el contenido encontrando la bandera y resolviendo la maquina.

___

## Procedimiento

Comence resolviendo las Tareas de la maquina, algunas de las tareas son pistas para resolver las maquina.

- **Tarea 1 ¿Qué puerto TCP está abierto en la máquina?**

`6379`

- **Tarea 2 ¿Qué servicio se está ejecutando en el puerto abierto en la máquina?**

`Redis`

- **Tarea 3 ¿Qué tipo de base de datos es Redis? Elija entre las siguientes opciones: (i) Base de datos en memoria, (ii) Base de datos tradicional**

`In-memory Database`

- **Tarea 4 ¿Qué utilidad de línea de comandos se utiliza para interactuar con el servidor Redis? Ingrese el nombre del programa que ingresaría en la terminal sin ningún argumento.**

`redis-cli`

- **Tarea 5 ¿Qué indicador se utiliza con la utilidad de línea de comandos de Redis para especificar el nombre de host?**

`-h`

- **Tarea 6 Una vez conectado a un servidor Redis, ¿qué comando se utiliza para obtener información y estadísticas sobre el servidor Redis?**

`Info`

- **Tarea 7 ¿Cuál es la versión del servidor Redis que se utiliza en la máquina de destino?**

`5.0.7`

- **Tarea 8 ¿Qué comando se utiliza para seleccionar la base de datos deseada en Redis?**

`Select`

- **Tarea 9 ¿Cuántas claves hay dentro de la base de datos con índice 0?**

`4`

- **Tarea 10 ¿Qué comando se utiliza para obtener todas las claves de una base de datos?**

`keys *`

- **Enviar Bandera Root**

Para encontrar la bandera realice un escaneo en nmap a la direccion ip, normalmente uso nmap con parametros basicos como `-sVC` y `-vvv` pero en esta maquina esos paramentros no fueron suficientes por lo que probe con nuevos y la linea quedo algo asi.

```bash
nmap -p- -sV -sC --open -sS -vvv -n -Pn 10.129.5.10 -oN escan

```
![Anexo1](/images/Redeemer/Anexo1.png)

Ya que el escaneo se completo con el comando `cat` listo lo que nos dejo el archivo `escan` para visualizar los resultados.

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
El escaneo me muestra que el puerto `6379` esta abierto corriendo un servicio `Redis` con version `5.0.7` por lo que me ayude del comando `redis-cli -h [DireccionIp]` para ingresar a la maquina.

![Anexo2](/images/Redeemer/Anexo2.png)

Con el comando `Info` veo toda la informacion de la maquina, tanto su version como sus bases y keys.

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
Ya que supe toda la informacion me quedo con lo que me interesa que seria lo que contiene `#Keyspace`.

``` bash
# Keyspace
db0:keys=4,expires=0,avg_ttl=0
(2.31s)
10.129.5.10:6379>

```
Con esta informacion supe que la `base de datos 0` contiene 4 keys por lo que con el comando `keys *` listo todas las keys existentes.

``` bash
10.129.5.10:6379> KEYS *
1) "stor"
2) "flag"
3) "temp"
4) "numb"
10.129.5.10:6379> 

```
Me fije que el literal `2` contiene el nombre de `flag` por lo que con el comando `get` listo su contenido.

``` bash
10.129.5.10:6379> GET flag
"03e1d2b376c37ab3f5319922053953eb"
10.129.5.10:6379> 

```
Ingreso la bandera en la ultima Tarea de la maquina `Enviar bandera`.

Una ves enviada la bandera salio un mensaje diciendo `Redeemer has been Pwned`.

![Anexo3](/images/Redeemer/Anexo3.png)
___

## Maquina Completada :)



