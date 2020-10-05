# ZelBench Commands

This page describes the available CLI commands for ZelNode Benchmarking Daemon

---

!!! note
    These commands are available when SSH'd into your ZelNode or through your VPS's dashboard/console

---

!!! example "List of Commands"
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

!!! example "Example Response"
    {  
    &#8199;&#8199;"version": "1.4.2",  
    &#8199;&#8199;"rpcport": 16224  
    }  

---

<b> getstatus</b> returns current connection status and ZelNode tier

```
zelbench-cli getstatus
```

!!! example "Example Response"
    {  
    &#8199;&#8199;"status": "online",  
    &#8199;&#8199;"benchmarking": "BAMF",  
    &#8199;&#8199;"zelback": "connected"  
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

!!! example "Example Response"
    {  
    &#8199;&#8199;"ipaddress": "YOURIPv4",  
    &#8199;&#8199;"status": "BAMF",  
    &#8199;&#8199;"time": 1586302461,  
    &#8199;&#8199;"cores": 8,  
    &#8199;&#8199;"ram": 32,  
    &#8199;&#8199;"ssd": 0,  
    &#8199;&#8199;"hdd": 4711.2998046875,  
    &#8199;&#8199;"ddwrite": 517.530029296875,  
    &#8199;&#8199;"eps": 1057.89794921875  
    }  

!!! warning
    It is OK if benchmarking is showing "hdd" instead of "ssd" for now. The "ddwrite" speeds telling the network that your drive(s) are SSDs

![zelbanner](/img/Banners/ZelComposite_BlackBG.png)
