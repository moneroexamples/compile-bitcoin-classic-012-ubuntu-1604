# Compile Bitcoin Classic on Xubuntu 16.04 x64 Beta 1
The example shows how to compile current github version of on [Bitcoin Classic](https://github.com/bitcoinclassic/bitcoinclassic), as of 4 March 2014 (version 0.12rc), on [Xubuntu 16.04 x64 Beta 1](http://www.omgubuntu.co.uk/2016/02/ubuntu-16-04-beta-1-download-flavors). Beta of Ubuntu 16.04 is not yet available. It will be released at the end of March.

More information about compilation of Bitcoin Classic can be found [here](https://github.com/bitcoinclassic/bitcoinclassic/blob/0.12/doc/build-unix.md). The official
Bitcoin Classic's binaries can be download from [here](https://github.com/bitcoinclassic/bitcoinclassic/releases).

## Dependencies
```bash
# install dependencies for Berkeley DB 4.8 and Bitcoin Classic
sudo apt-get install git build-essential cmake libboost-all-dev autoconf libtool zlibc libssl-dev pkg-config libevent-dev bsdmainutils libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler libqrencode-dev
```

## Compile Berkeley DB 4.8
Before proceeding with the compilation, the Berkeley DB 4.8 is required. Its currently
not available in Ubuntu 16.04 repositories, thus we need to compile it ourselves.

```bash
#download berkeley-db 4.8 source code
wget http://download.oracle.com/berkeley-db/db-4.8.30.tar.gz

# unpack and enter unix folder
tar -xzvf db-4.8.30.tar.gz && cd db-4.8.30/build_unix/

# configure for compilation
../dist/configure --enable-cxx --disable-shared --with-pic --prefix="/opt/bdb48/"

# compile
make # or make -j number_of_threads, e.g., make -j 2

# install in /opt/bdb48/
sudo make install
```

This should result in the following folder tree in `/opt/bdb48`:

```bash
/opt/bdb48/
├── bin
│   ├── db_archive
│   ├── db_checkpoint
│   ├── db_deadlock
│   ├── db_dump
│   ├── db_hotbackup
│   ├── db_load
│   ├── db_printlog
│   ├── db_recover
│   ├── db_sql
│   ├── db_stat
│   ├── db_upgrade
│   └── db_verify
├── docs
│   ├── api_reference
│   ├── articles
│   ├── collections
│   ├── csharp
│   ├── gsg
│   ├── gsg_db_rep
│   ├── gsg_txn
│   ├── index.html
│   ├── java
│   ├── license
│   ├── porting
│   └── programmer_reference
├── include
│   ├── db_cxx.h
│   └── db.h
└── lib
	├── libdb-4.8.a
	├── libdb.a
	├── libdb_cxx-4.8.a
	└── libdb_cxx.a
```

## Bitcoin Classic compilation and installation
Having the dependencies, we can download the current Bitcoin Classic version and compile it as follows:

```bash
# download the latest Bitcon Classic source code from github
git clone https://github.com/bitcoinclassic/bitcoinclassic.git

# go into bitmonero folder
cd bitcoinclassic/

# preparing Bitcion build system for compilation
./autogen.sh

# configure compilation to use Berkeley DB and to install binaries in /opt/bitcoinclassic/
./configure LDFLAGS="-L/opt/bdb48/lib/" CPPFLAGS="-I/opt/bdb48/include/" --prefix="/opt/bitcoinclassic/"

# compile
make # or make -j number_of_threads, e.g., make -j 2

# install in /opt/bitcoinclassic/
sudo make install
```

After successful compilation and installation we should get the the following bineries
in `/opt/bitcoinclassic/`:

```bash
/opt/bitcoinclassic/
├── bin
│   ├── bench_bitcoin
│   ├── bitcoin-cli
│   ├── bitcoind
│   ├── bitcoin-qt
│   ├── bitcoin-tx
│   ├── test_bitcoin
│   └── test_bitcoin-qt
├── include
│   └── bitcoinconsensus.h
└── lib
	├── libbitcoinconsensus.a
	├── libbitcoinconsensus.la
	├── libbitcoinconsensus.so -> libbitcoinconsensus.so.0.0.0
	├── libbitcoinconsensus.so.0 -> libbitcoinconsensus.so.0.0.0
	├── libbitcoinconsensus.so.0.0.0
	└── pkgconfig
    	└── libbitcoinconsensus.pc
```
## Run Bitcoin Classic

After that, you can run your the Bitcoin Classic GUI `/bitcoin-qt`.

```bash
# launch the Bitcoin Classic GUI
/opt/bitcoinclassic/bin/bitcoin-qt
```

## Screenshot

![Xubuntu screenshot](https://raw.githubusercontent.com/moneroexamples/compile-bitcoin-classic-11-2-xubuntu-1604-beta-1/master/img/xubuntu_screenshot.jpg)


## Other examples
Other examples can be found on  [github](https://github.com/moneroexamples?tab=repositories).
Please know that some of the examples/repositories are not
finished and may not work as intended.


## How can you help?
Constructive criticism, code and website edits are always good. They can be made through github.

Some Monero are also welcome:
```
48daf1rG3hE1Txapcsxh6WXNe9MLNKtu7W7tKTivtSoVLHErYzvdcpea2nSTgGkz66RFP4GKVAsTV14v6G3oddBTHfxP6tU
```
