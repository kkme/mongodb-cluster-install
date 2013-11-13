mongodb-data
============
Config files and data folders for mongodb-10gen cluster and simple cluster setup deployment scripts.

Run all scripts as root.
* `deploy-master-full.sh`   install and run simple mongodb cluster: one router, 3 config servers and one shard (all one the same machine).
* `deploy-master-test.sh`   install and run test mongodb cluster: one router, 1 config server and one shard (all one the same machine).
* `deploy-shard.sh`    install and run mongodb cluster shard (run one separate machine).
* `run-master-full.sh` run full cluster setup (with 3 config servers).
* `run-master-test.sh` run test cluster setup (with 1 config server).
* `run-shard.sh`       run single shard.

Installation & deployment
-------------------------
To deploy mongodb-10gen test cluster on a single machine with a single shard, run as superuser:
```sh
git clone https://github.com/roveo/mongodb-data.git /data
sh /data/deploy-master-test.sh
```
Enter username which mongodb cluster will run under when prompted.

_No security or sharding is enabled by default._

Additional shards
-----------------
To deploy a single shard on another machine, run:
```sh
git clone https://github.com/roveo/mongodb-data.git /data
sh /data/deploy-shard.sh
```

After that run on master:
```sh
mongo --eval "sh.addShard('{shard_ip}:27037')"
```

Info
----
`mongos` instance is running on default port and two interfaces: loopback `127.0.0.1` and public interface, so the cluster is available with just `mongo` command.

Three config servers are running on ports 27027-27029.

Shards are running on port 27037, one shard per computer (including master) is presumed.