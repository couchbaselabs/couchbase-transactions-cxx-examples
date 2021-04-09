# Couchbase Distributed Transactions Examples for C++

## Game Example

This example is based on the Game Simulation sample bucket provided with Couchbase.
You will not need to install the sample bucket to run this.

There are two entities, Player and Monster.  To keep things simple, we just create one of each
and have the player deal damage to the monster until it runs out of hit points.  Each time the
player deals damage to the monster, we update both documents in a transaction.

Of course, with only one thread doing this, we don't need transactions at all.  But the code
demonstrates how one would use transactions in c++.

### Building
You will need the transactions library -- see [docs](https://docs.couchbase.com/cxx-txns/current/distributed-acid-transactions-from-the-sdk.html) for details.
Then, clone this library (if you haven't already), create a build directory and build...

```
git clone git@github.com:couchbaselabs/couchbase-transactions-cxx-examples.git
cd couchbase-transactions-cxx-examples/game/
mkdir build && cd build
cmake ../
make
```

### Running
By default, `game_server` assumes localhost for the couchbase server, with user `Administrator`, password `password`, and `default` for the bucket to use.  However,
You can specify them all as positional arguments: `game_server <host> <user> <pass> <bucket>`.  For example:
```
./game_server 10.1.1.1 localhost someuser somepass
```
This uses the host at `10.1.1.1`, user `someuser` with password `somepass`.  And the `default` bucket, since no 4th parameter was specified.

You will see logging output, and the game quickly ends.  You can change the monster's hitpoints, amount of damage, etc... and rebuild to see the effects.
