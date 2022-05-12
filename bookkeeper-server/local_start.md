## start bookkeeper local
* entrance class is org.apache.bookkeeper.server.Main or `bookkeeper bookie`
* log4j issue (solved in branch-3.15)
* zk Node does not exist ? (parent node must have been created)
* command lile params
```aidl
-c
conf/bk_server.conf
-z
localhost:2181
-m
/bk/ledgers
-p
3181
-j
~/workspace/bookeeper-data/bk1/journal
-i
~/workspace/bookeeper-data/bk1/index1
~/workspace/bookeeper-data/bk1/index2
-l
~/workspace/bookeeper-data/bk1/ledger1
~/workspace/bookeeper-data/bk1/ledger2
```
* it has 2 ports, one is nettyBookieServer, one is httpServer.
* sourcecode of bkctl is in BKCommand.apply, it is abstrct, subclass impl it.
* mac port usage "lsof -i tcp:8080"
* zookeeper admin server "localhost:8080/commands" to see all commands, it only serve GET requests.
* bookkeeper httpServer route info is in HttpRouter.
* `bookkeeper shell` is also a command line tool. sourcecode is in BookieShell and BookieShell.Command.

## start LocalBookkeeper
* LocalBookKeeper or `bookkeeper localbookie`
* program arguments
```aidl
5
conf/bk_server.conf
/Users/yapxue/workspace/bookeeper-data/localbk
```
or execute `./bookkeeper localbookie 5 /Users/yapxue/workspace/bookeeper-data/localbk`
* make some changes to `conf/bk_server.conf`, specify ledgerDir, indexDir.
* journalDir is something like `/var/folders/06/7cfc5v9d7n35zsrfnrjlpw7039d0sy/T/localbookkeeper03533104557498308953test`. 
* java.lang.ClassNotFoundException: com.codahale.metrics.Reservoir, org.xerial.snappy.SnappyInputStream. It is becauseof misssing some zookeeper dendency. change pom scope from test to compile.
* use zkcli to list all bookies.
* httpServer is not started.
* bkctl use the same config file with bookieServer, it should be executed on server or give a env CLI_CONF. `bookkeeper shell` can also override default config by system env.
