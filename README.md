# Citus [zfs]
improved ZFS performance, pg configure add:

* --with-blocksize=32
* --with-wal-blocksize=64

### zfs setting

```
ZFS_POOL_NAME=data4
MOUNT_POINT_DIR=/mnt/data4

sudo zfs create $ZFS_POOL_NAME/pg_data -o mountpoint=$MOUNT_POINT_DIR/pg_data

sudo chmod 0750 $MOUNT_POINT_DIR/pg_data

sudo zfs set recordsize=128k $ZFS_POOL_NAME/pg_data
sudo zfs set compression=zstd $ZFS_POOL_NAME/pg_data
sudo zfs set atime=off $ZFS_POOL_NAME/pg_data
sudo zfs set xattr=sa $ZFS_POOL_NAME/pg_data
sudo zfs set logbias=latency $ZFS_POOL_NAME/pg_data
sudo zfs set redundant_metadata=most $ZFS_POOL_NAME/pg_data
```

### postgres setting

```
# postgresql.conf
full_page_writes = off
```

## build

**citus:11.3.0-alpine**

```
docker build -t postgres:15.2-alpine postgres15.2-alpine/
docker build -t citus:11.3.0-alpine  citus11.3.0-alpine/ --pull=false
```

**citus:12.1.0-alpine**

```
docker build -t postgres:16.0-alpine postgres16.0-alpine/
docker build -t citus:12.1.0-alpine  citus12.1.0-alpine/ --pull=false
```

## push ghcr

```
export GITHUB_TOKEN=
export GITHUB_USER=zzir
export CITUS_TAG=citus:12.1.0-alpine

echo $GITHUB_TOKEN | docker login ghcr.io -u $GITHUB_USER --password-stdin
docker tag $CITUS_TAG ghcr.io/$GITHUB_USER/$CITUS_TAG
docker push ghcr.io/$GITHUB_USER/$CITUS_TAG
```
