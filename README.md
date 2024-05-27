# ElectrumX - Bit7 Adapted

  :License: MIT
  :Language: Python (>= 3.8)
  :Original Author: Neil Booth

This project is a fork of `kyuupichan/electrumx <https://github.com/kyuupichan/electrumx>`_.
The original author dropped support for Bitcoin, which we intend to keep.

ElectrumX allows users to run their own Electrum server. It connects to your
full node and indexes the blockchain, allowing efficient querying of the history of
arbitrary addresses. The server can be exposed publicly, and joined to the public network
of servers via peer discovery. As of May 2020, a significant chunk of the public
Electrum server network runs ElectrumX.

Documentation
=============
See `readthedocs <https://electrumx-spesmilo.readthedocs.io/>`_.

Setup:
======
1- Install Dependencies
```
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-pip python3-venv build-essential libssl-dev git
```

2- Create and activate a Python virtual environment:
```
python3 -m venv electrumx-venv
source electrumx-venv/bin/activate
```

3- Install ElectrumX:
```
pip install uvloop
pip install -e .
```

4- Create ElectrumX Database directory (Change choose any preferred directory):
```
mkdir -p /electrumxdb_bit7/
```


4- Create the ElectrumX Configuration File (Preferibly at ``/etc/electrumx_bit7.conf``:
```
DB_DIRECTORY = /electrumxdb_bit7/
COIN = Bit7
DAEMON_URL = http://RPC_USERNAME:RPC_PASSWORD@RPC_HOST:15533/
SERVICES = tcp://:7707,rpc://:7007
```

5- Create ElectrumX Service (At /etc/systemd/system/electrumx.service):
```
[Unit]
Description=ElectrumX Bit7 Server
After=network.target

[Service]
EnvironmentFile=/etc/electrumx_bit7.conf
ExecStart=/path/to/electrumx-venv/bin/electrumx_server -c /etc/electrumx_bit7.conf
User=linuxuser #Change with the user of this linux
LimitNOFILE=8192
TimeoutStopSec=30min

[Install]
WantedBy=multi-user.target
```


6- Reload service:
```
sudo systemctl daemon-reload
sudo systemctl enable electrumx
```

7- Start ElectrumX Service:
```
sudo systemctl start electrumx
```

### Note: You might face a problem with the environment like "DB_DIRECTORY" not in env, then just set the content of electrumx_bit7.conf universally as ENV. VARIABLES.


