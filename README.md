# mongodb-cluster-install
Script for nice and simple installation of mongodb-10gen sharded cluster.

## Install
There are two prerequisites:
* you must have an empty data folder owned by the same user that will run the cluster
* you must run the script from this user

In the example below we use the folder we clone the installation script into `/data` folder. Because we do it as a superuser (`sudo` before the command), the folder is owned by `root` user. After cloning the repo we have to set folder owner to the user that will run the cluster (`mongodb` in the example). Then we run the installation script and run the minimal cluster setup as `mongodb` user.

```sh
# clone installation script into /data folder
sudo git clone https://github.com/roveo/mongodb-cluster-install.git /data
sudo chown mongodb /data # set owner to mongodb
sudo -u mongodb /data/install
sudo -u mongodb /data/run-min
```

## Additional shards
-----------------
To run a single shard on another machine, run:
```sh
sudo -u mongodb /data/run-shard
```
instead of the last line.

After that run on master:
```sh
mongo --eval "sh.addShard('{shard_ip}:27037')"
```

Info
----
`mongos` instance is running on default port and two interfaces: loopback `127.0.0.1` and public interface, so the cluster is available with just `mongo` command.

Three config servers are running on ports 27027-27029.

Shards are running on port 27037, one shard per computer (including master) is presumed.

For more information on mongodb sharded clusters, see the docs: http://docs.mongodb.org/manual/sharding/