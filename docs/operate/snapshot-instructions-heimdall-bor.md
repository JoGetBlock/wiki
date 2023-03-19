---
id: snapshot-instructions-heimdall-bor
title: Heimdall and Bor Snapshots
description: Heimdall and Bor snapshot Instructions for faster syncing.
keywords:
  - docs
  - matic
  - polygon
  - binary
  - node
  - validator
  - sentry
  - heimdall
  - bor
  - snapshots
image: https://wiki.polygon.technology/img/polygon-logo.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

When setting up a new sentry, validator, or full node server, it is recommended that you use a snapshot for faster syncing without having to sync over the network. Using snapshots will save you several days for both Heimdall and Bor.

:::tip

For the latest snapshot, please visit [<ins>Polygon Chains Snapshots</ins>](https://snapshot.polygon.technology/).

:::

## Heimdall Snapshot

First, you need to set up your node with **prerequisites** as per the node setup guide. Before you start services for Heimdall to sync, follow the steps below to use the snapshot:

1. Download the snapshot tar file of Heimdall on your VM by running the following command:

```
aria2c -x6 -s6  <snapshot_url>

// For example, this will download the snapshot of Heimdall:
aria2c -x6 -s6 https://matic-blockchain-snapshots.s3-accelerate.amazonaws.com/matic-mainnet/heimdall-mainnet-fullnode-2023-03-04.tar.zst
```

2. To unpack the tar file in the Heimdall data directory, run the following command:
```
// install decompression and progress bar dependencies
sudo apt-get update -y
sudo apt-get install -y zstd
sudo apt-get install -y pv

// You must ensure you are running this command before you start the Heimdall service on your node.
// If your Heimdall service has started, please stop the service and run the following command.
// Once unpacking is complete, you can start the Heimdall service again.
pv <snapshot file> | tar -I zstd -xf - -C <HEIMDALL_DATA_DIRECTORY>

// If your Heimdall data directory is different,
// please replace the directory name in the command for starting the Heimdall service.
// When this command completes, you may delete the tar file to reclaim space.

// For example, this will unpack the tar file in the Heimdall Data directory with progress bar:
pv heimdall-mainnet-fullnode-2023-03-04.tar.zst | tar -I zstd -xf - -C /var/lib/heimdall/data/
```

## Bor Snapshot

First, you need to set up your node with **prerequisites**, as per the node setup guide. Before you start services for Bor to sync, follow the steps below to use the snapshot:

1. Download the snapshot tar file of Bor on your VM by running the following command:
```
aria2c -x6 -s6  <snapshot_url>

// For example, this will download the snapshot of Heimdall:
aria2c -x6 -s6 https://matic-blockchain-snapshots.s3-accelerate.amazonaws.com/matic-mainnet/bor-mainnet-fullnode-2023-03-04.tar.zst
```

2. To unpack the tar file in the Bor Data directory, run the following command:

```
// You must ensure you are running this command before you start the Bor service on your node.
// If your Bor service has started, please stop the service and run the following command:
// Once unpacking is complete, you can start the Bor service again.
pv <snapshot file>  | tar -I zstd -xf - -C <BOR_DATA_DIRECTORY>

// If your bor data directory is different
// please replace the directory name in the command for starting the Bor service.
// When this command completes, you may delete the tar file to reclaim space.

// For example, this will unpack the tar file in the Bor data directory:
pv bor-mainnet-fullnode-2023-03-04.tar.zst | tar -I zstd -xf - -C /var/lib/bor/data/bor/chaindata
```

:::note

The `aria2c` method is used for downloading snapshots faster.
There is an alternate way where the downloaded snapshots can be directly extracted without any intervention.

**Steps for that:**


```bash title="For Heimdall"
wget -c https://matic-blockchain-snapshots.s3-accelerate.amazonaws.com/matic-mainnet/heimdall-mainnet-fullnode-2023-03-04.tar.zst -O - | tar -I zstd -xf - -C /var/lib/heimdall/data/
```

```bash title="For Bor"
wget -c     https://matic-blockchain-snapshots.s3-accelerate.amazonaws.com/matic-mainnet/bor-mainnet-fullnode-2023-03-04.tar.zst -O - | tar -I zstd -xf - -C /var/lib/bor/data/bor/chaindata
```
:::