# Configuration

This document explains the configurable properties of the node. Klaytn node package ships with good defaults and requires very little configuration. If you changed any settings of a running node, you must restart the node to reflect the changes.

## CN Configuration File location <a href="#cn-configuration-file-location" id="cn-configuration-file-location"></a>

* `kcnd.conf` for configuring the Consensus Node

The configuration file is located in the `conf` directory, whose default location depends on whether or not the installation is from an archive distribution (`tar.gz`) or a package distribution (RPM).

* For the archive distribution, the config directory location defaults to `$INSTALL_PATH/kcn-linux-amd64/conf/`.
* For the package distribution, the config directory defaults to `/etc/kcnd/conf/`.

## PN Configuration File location <a href="#pn-configuration-file-location" id="pn-configuration-file-location"></a>

* `kpnd.conf` for configuring the Proxy Node

The configuration file is located in the `conf` directory, whose default location depends on whether or not the installation is from an archive distribution (`tar.gz`) or a package distribution (RPM).

* For the archive distribution, the config directory location defaults to `$INSTALL_PATH/kpn-linux-amd64/conf/`.
* For the package distribution, the config directory defaults to `/etc/kpnd/conf/`.

## EN Configuration File location <a href="#configuration-file-location" id="configuration-file-location"></a>

* `kend.conf` for configuring the Endpoint Node

The configuration file is located in the `conf` directory, whose default location depends on whether or not the installation is from an archive distribution (`tar.gz`) or a package distribution (RPM).

* For the archive distribution, the config directory location defaults to `$INSTALL_PATH/ken-linux-amd64/conf/`.
* For the package distribution, the config directory defaults to `/etc/kend/conf/`.

## Configuration File Format <a href="#configuration-file-format" id="configuration-file-format"></a>

CN and PN have the same configuration file format and the properties.

Below is a sample configuration file for the CN that participates in the `cypress` network and stores the blockchain data in the default location, which is `~/kcnd_home` with the archive distribution, `/var/kcnd/data` with the package distribution.

```
# Configuration file for the kcnd

# cypress, baobab is only available if you don't specify NETWORK_ID.
NETWORK="cypress"
# if you specify NETWORK_ID, a private network is created.
NETWORK_ID=
PORT=32323
SERVER_TYPE="fasthttp"
SYNCMODE="full"
VERBOSITY=3
MAXCONNECTIONS=100
# LDBCACHESIZE=10240
REWARDBASE="0x0"

...

DATA_DIR=
LOG_DIR=$DATA_DIR/logs
```

The recommended txpool sizes for CN are as follows.

```
TXPOOL_EXEC_SLOTS_ALL=16384
TXPOOL_NONEXEC_SLOTS_ALL=16384
TXPOOL_EXEC_SLOTS_ACCOUNT=16384
TXPOOL_NONEXEC_SLOTS_ACCOUNT=16384
```

The recommended txpool sizes for PN are as follows.

```
TXPOOL_EXEC_SLOTS_ALL=8192
TXPOOL_NONEXEC_SLOTS_ALL=8192
TXPOOL_EXEC_SLOTS_ACCOUNT=8192
TXPOOL_NONEXEC_SLOTS_ACCOUNT=8192
```

The recommended txpool sizes for EN are as follows.

```
TXPOOL_EXEC_SLOTS_ALL=4096
TXPOOL_NONEXEC_SLOTS_ALL=4096
TXPOOL_EXEC_SLOTS_ACCOUNT=4096
TXPOOL_NONEXEC_SLOTS_ACCOUNT=4096
```

## Properties <a href="#properties" id="properties"></a>

The configuration file has the following configurable properties. CN and PN configuration files have the same properties except `REWARDBASE.`

| Name                            | Description                                                                                                                                                                                                                                                       |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NETWORK                         | Network name that this node will join. This value is used when NETWORK\_ID is not defined. ("cypress", "baobab")                                                                                                                                                  |
| NETWORK\_ID                     | <p>Klaytn network ID. If you create a local private network, you will define the network ID for your own. Following IDs are reserved for pre-configured networks.<br>8217 : Cypress (Main network)<br>1000 : Aspen test network<br>1001 : Baobab test network</p> |
| PORT                            | P2P port. (Default: "32323")                                                                                                                                                                                                                                      |
| SERVER\_TYPE                    | JSON RPC server type. ("http", "fasthttp")                                                                                                                                                                                                                        |
| SYNCMODE                        | Blockchain sync mode. ("fast", "full")                                                                                                                                                                                                                            |
| VERBOSITY                       | Logging verbosity. (0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail)                                                                                                                                                                                         |
| MAXCONNECTIONS                  | Maximum number of physical connections. All single-channel peers can have up to MAXCONNECTIONS peers. All multi-channel peers can have up to MAXCONNECTIONS/2 peers. Network connection is disabled if it is set to 0. (Default: 10)                              |
| LDBCACHESIZE                    | Size of in-memory cache in LevelDB (MiB). (Default : 768)                                                                                                                                                                                                         |
| REWARDBASE                      | Account address that will receive block consensus rewards. This property only applies to CN.                                                                                                                                                                      |
| TXPOOL\_EXEC\_SLOTS\_ALL        | Maximum number of executable transaction slots for all accounts. (Default: 4096)                                                                                                                                                                                  |
| TXPOOL\_NONEXEC\_SLOTS\_ALL     | Maximum number of non-executable transaction slots for all accounts. (Default: 1024)                                                                                                                                                                              |
| TXPOOL\_EXEC\_SLOTS\_ACCOUNT    | Number of executable transaction slots guaranteed per account. (Default: 16)                                                                                                                                                                                      |
| TXPOOL\_NONEXEC\_SLOTS\_ACCOUNT | Maximum number of non-executable transaction slots guaranteed per account. (Default: 64)                                                                                                                                                                          |
| TXPOOL\_LIFE\_TIME              | Maximum amount of time non-executable transactions is queued. (Default : 5m)                                                                                                                                                                                      |
| RPC\_ENABLE                     | Enable the HTTP-RPC server if it is set to 1.                                                                                                                                                                                                                     |
| RPC\_API                        | Comma-separated list of APIs offered over the HTTP-RPC interface. (admin, debug, klay, miner, net, personal, rpc, txpool, web3)                                                                                                                                   |
| RPC\_PORT                       | HTTP-RPC server listening port. (Default: "8551")                                                                                                                                                                                                                 |
| RPC\_ADDR                       | HTTP-RPC server listening interface. (Default: "localhost")                                                                                                                                                                                                       |
| RPC\_CORSDOMAIN                 | Comma-separated list of domains from which to accept cross-origin requests (browser enforced)                                                                                                                                                                     |
| RPC\_VHOSTS                     | Comma-separated list of virtual hostnames from which to accept requests (server enforced). Accepts '\*' wildcard. (Default: {"localhost"})                                                                                                                        |
| WS\_ENABLE                      | Enable the WS-RPC server if it is set to 1.                                                                                                                                                                                                                       |
| WS\_API                         | APIs offered over the WS-RPC interface. (admin, debug, klay, miner, net, personal, rpc, txpool, web3)                                                                                                                                                             |
| WS\_ADDR                        | WS-RPC server listening interface.                                                                                                                                                                                                                                |
| WS\_PORT                        | WS-RPC server listening port. (Default : "8552")                                                                                                                                                                                                                  |
| WS\_ORIGINS                     | Origins from which to accept websockets requests. (Default: "localhost")                                                                                                                                                                                          |
| AUTO\_RESTART                   | Restart the process when the current block has not been updated for `autorestart.timeout` (e.g., 60s, 10m and 1h) if it is set to 1.                                                                                                                              |
| METRICS                         | Enable metrics collection and reporting if it is set to 1.                                                                                                                                                                                                        |
| PROMETHEUS                      | Enable prometheus exporter if it is set to 1.                                                                                                                                                                                                                     |
| DB\_NO\_PARALLEL\_WRITE         | Disable parallel writes of block data to persistent database if it is set to 1.                                                                                                                                                                                   |
| MULTICHANNEL                    | Create a dedicated channel for block propagation if it is set to 1.                                                                                                                                                                                               |
| SUBPORT                         | Listening sub port number if multichannel option is enabled. (Default : "32324")                                                                                                                                                                                  |
| NO\_DISCOVER                    | Turn off the discovery option if it is set to 1.                                                                                                                                                                                                                  |
| BOOTNODES                       | Comma-separated kni addresses of bootstrap nodes.                                                                                                                                                                                                                 |
| ADDITIONAL                      | For additional command-line options. e.g) --txpool.nolocals                                                                                                                                                                                                       |
| DATA\_DIR                       | Klaytn blockchain data folder path.                                                                                                                                                                                                                               |
| LOG\_DIR                        | Log folder path.                                                                                                                                                                                                                                                  |