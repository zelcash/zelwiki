# ZelBench Commands

This page describes the available CLI commands for ZelNode Benchmarking Daemon

---

!!! tip
    These commands are available when SSH'd into your ZelNode or through your VPS's dashboard/console

---

### List of Commands

* getinfo
* getstatus
* signzelnodetransactions
* restartnodebenchmarks
* getbenchmarks

### Command Explanations

<b> getinfo </b> returns general zelbench daemon info

```
zelbench-cli getinfo
```

!!! example
    {
        "version": "1.1.0",
        "rpcport": 16224
    }

---

<b> getstatus</b> returns current connection status and ZelNode tier

```
zelbench-cli getstatus
```

!!! example
    {
        "status": "online",
        "benchmarking": "BAMF",
        "zelback": "connected"
    }

---

<b> signzelnodetransaction</b> Command to get benchmarkd to sign a zelnode broadcast
```
zelbench-cli signzelnodebroadcast "HEXSTRING"
```

!!! info
    "HEXSTRING" - (string) The hex encoded zelnode broadcast message

---

<b> restartnodebenchmarks</b> re-run ZelNode benchmarking tests

```
zelbench-cli restartnodebenchmarks
```

!!! info
    ZelNode will re-run performance tests for hardware configuration, drive write speeds, and CPU calculation speeds

---

<b> getbenchmarks</b> output latest benchmarking scores
```
zelbench-cli getbenchmarks
```

!!! example
    {<br>
        "ipaddress": "YOURIPv4",<br>
        "status": "BAMF",<br>
        "time": 1586302461,<br>
        "cores": 8,<br>
        "ram": 32,<br>
        "ssd": 0,<br>
        "hdd": 4711.2998046875,<br>
        "ddwrite": 517.530029296875,<br>
        "eps": 1057.89794921875<br>
    }

!!! warning
    It is OK if benchmarking is showing "hdd" instead of "ssd" for now. The "ddwrite" speeds telling the network that your drive(s) are SSDs

![zelbanner](/img/ZelComposite_BlackBG.png)
