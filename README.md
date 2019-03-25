# phoenix-miner

PhoenixMiner is Ethash (**ETH, ETC, Muiscoin, EXP, UBQ, etc.**) miner that **supports both AMD and Nvidia** cards (including in mixed mining rigs). It runs under Windows x64 and Linux x64 and has a developer **fee of 0.65%**. This means that every 90 minutes the miner will mine for us, its developers, for 35 seconds.

PhoenixMiner also supports Ubqhash for mining UBQ, ProgPOW for mining BCI, and dual mining Ethash/Ubqhash with Blake2s.

<h2>Features, requirements, and limitations</h2>

* Supports AMD Vega, 580/570/480/470, 460/560, Fury, 390/290 and older AMD GPUs with enough VRAM
* Supports Nvidia 20x0, 10x0 and 9x0 series as well as older cards with enough VRAM
* Highly optimized OpenCL and CUDA cores for maximum ethash mining speed
* Optional "green" kernels for RX580/570/560/480/470/460 to lower the power consumption by 2-3% with small, or no drop in hashrate
* Lowest developer fee of 0.65% (35 seconds defvee mining per each 90 minutes)
* Dual mining ethash/Blake2s with lowest devfee of 0.9% (35 seconds defvee mining per each 65 minutes)
* Advanced statistics: actual difficulty of each share, effective hashrate at the pool, and optional showing of estimated income in USD
* DAG file generation in the GPU for faster start-up and DAG epoch switches
* Supports all ethash mining pools and stratum protocols
* Supports secure pool connections (e.g. ssl://eu1.ethermine.org:5555) to prevent IP hijacking attacks
* Detailed statistics, including the individual cards hashrate, shares, temperature and fan speed
* Unlimited number of fail-over pools in epools.txt configuration file (or two on the command line)
* Automatic GPU tuning for the AMD GPUs to achieve maximum performance with your rig
* Supports devfee on alternative ethash currencies like ETC, EXP, Music, UBQ, Pirl, Ellaism, Metaverse ETP, PGC, Akroma, WhaleCoin, Victorium, Nekonium, Mix, EtherGem, Aura, HBC, Genom, EtherZero, Callisto, DubaiCoin, MOAC, Ether-1, and EtherCC. This allows you to use older cards with small VRAM or low hashate on current DAG epochs (e.g. GTX970).
* Full compatibility with the industry standard Claymore's Dual Ethereum miner, including most of command-line options, configuration files, and remote monitoring and management.
* Supports the new Ubqhash algorithm for the UBQ coin. Please note that you must add -coin ubq to your command line (or COIN: ubq to your epools.txt file) in order to mine UBQ
* Supports the ProgPOW algorithm for the Bitcoin Interest (BCI) coin mining. Please note that you must add -coin bci to your command line (or COIN: bci to your epools.txt file) in order to mine BCI
* Supports the ProgPOW algorithm for mining BCI.
* More features coming soon!

<h2>Command-line arguments</h2>

Note that PhoenixMiner supports most of the command-line options of Claymore's dual Ethereum miner
so you can use the same command line options as the ones you would have used with Claymore's miner.

<h3>Pool options:</h3>

``` 
-pool <host:port> Ethash pool address (prepend the host name with ssl:// for SSL pool, or http:// for solo mining)
-wal <wallet> Ethash wallet (some pools require appending of user name and/or worker)
-pass <password> Ethash password (most pools don't require it, use 'x' as password if unsure)
-worker <name> Ethash worker name (most pools accept it as part of wallet)
-proto <n> Selects the kind of stratum protocol for the ethash pool:
     1: miner-proxy stratum spec (e.g. coinotron)
     2: eth-proxy (e.g. dwarfpool, nanopool) - this is the default, works for most pools
     3: qtminer (e.g. ethpool)
     4: EthereumStratum/1.0.0 (e.g. nicehash)
     5: EthereumStratum/2.0.0
-coin <coin> Ethash coin to use for devfee to avoid switching DAGs:
     auto: Try to determine from the pool address (default)
     eth: Ethereum
     etc: Ethereum Classic
-stales <n> Submit stales to ethash pool: 1 - yes (default), 0 - no
-pool2 <host:port>  Failover ethash pool address. Same as -pool but for the failover pool
-wal2 <wallet> Failover ethash wallet (if missing -wal will be used for the failover pool too)
-pass2 <password> Failover ethash password (if missing -pass will be used for the failover pool too)
-worker2 <name> Failover ethash worker name (if missing -worker will be used for the failover pool too)
-proto2 <n> Failover ethash stratum protocol (if missing -proto will be used for the failover pool too)
-coin2 <coin> Failover devfee Ethash coin (if missing -coin will be used for the failover pool too)
-stales2 <n> Submit stales to the failover pool: 1 - yes (default), 0 - no
-dpool <host:port> Dual mining pool address
-dwal <wallet> Dual mining wallet
-dpass <password> Dual mining pool password (most pools don't require it, use 'x' as password if unsure)
-dworker <name> Dual mining worker name
-dcoin blake2s Currently only the Blake2s algorithm is supported for dual mining. 
-dstales <n> Submit stales to the dual mining pool: 1 - yes (default), 0 - no
```

<h3>General pool options:</h3>

``` 
-fret <n> Switch to next pool afer N failed connection attempts (default: 3)
-ftimeout <n> Reconnect if no new ethash job is receved for n seconds (default: 600)
-ptimeout <n> Switch back to primary pool after n minutes. This setting is 30 minutes by default;
              set to 0 to disable automatic switch back to primary pool.
-retrydelay <n> Seconds to wait before reconnecting (default: 20)
-gwtime <n> Recheck period for Solo/GetWork mining (default: 200 ms)
-rate <n> Report hashrate to the pool: 1 - yes, 0 - no (1 is the default)
```


<h3>General Options:</h3>

```
  -v,--version  Show the version and exit
  -vs Show short version string (e.g. "4.1c") and exit
  -h,--help  Show information about the command-line options and exit
  -log <n> Selects the log file mode:
     0: disabled - no log file will be written
     1: write log file but don't show debug messages on screen (default)
     2: write log file and show debug messages on screen
  -logfile <name> Set the name of the logfile. If you place an asterisk (*) in the logfile name, it will be
      replaced by the current date/time to create a unique name every time PhoenixMiner is started. If there
      is no asterisk in the logfile name, the new log entries will be added to end of the same file. If you
      want to use the same logfile but the contents to be overwritten every time when you start the miner,
      put a dollar sign ($) character in the logfile name (e.g. -logfile my_log.txt$).
  -logdir <path> Set a path where the logfile(s) will be created
  -logsmaxsize <n> Maximum size of the logfiles in MB. The default is 200 MB (use 0 to turn off the limitation).
      On startup, if the logfiles are larger than the specified limit, the oldest are deleted. If you use a
      single logfile (by using -logfile), then it is truncated if it is bigger than the limit and a new one
      is created.
  -timeout <n> Restart miner according to -rmode after n minutes
  -pauseat <hh:mm> Pause the miner at hh::mm (24 hours time). You can specify multiple times: -pauseat 6:00,12:00
  -resumeat <hh:mm> Resume the miner at hh::mm (24 hours time). You can specify multiple times: -resumeat 8:00,22:0
  -fanmin <n> Set fan control min speed in % (-1 for default)
  -fanmax <n> Set fan control max speed in % (-1 for default)
  -fcm <n> Set fan control mode (0 - auto, 1 - use VBIOS fan control, 2 - forced fan control; default: 0)
  -tmax <n> Set fan control max temperature (0 for default)
  -powlim <n> Set GPU power limit in % (from -75 to 75, 0 for default)
  -cclock <n> Set GPU core clock in MHz (0 for default)
  -cvddc <n> Set GPU core voltage in mV (0 for default)
  -mclock <n> Set GPU memory clock in MHz (0 for default)
  -mvddc <n> Set GPU memory voltage in mV (0 for default)
  -tstop <n> Pause a GPU when temp is >= n deg C (0 for default; i.e. off)
  -tstart <n> Resume a GPU when temp is <= n deg C (0 for default; i.e. off)
```
>** MORE MINER OPTIONS YOU CAN FIND [HERE](https://bitcointalk.org/index.php?topic=2647654.0)  - official Phoenix Miner developers thread**


