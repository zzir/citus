improved ZFS performance, pg configure add:

* --with-blocksize=32
* --with-wal-blocksize=64

### citus:11.3.0-alpine

```
docker build -t postgres:15.2-alpine postgres15.2-alpine/
docker build -t citus:11.3.0-alpine  citus11.3.0-alpine/ --pull=false
```

### codespace build

```
export GITHUB_TOKEN=
export GITHUB_USER=zzir

echo $GITHUB_TOKEN | docker login ghcr.io -u $GITHUB_USER --password-stdin
docker tag citus:11.3.0-alpine ghcr.io/$GITHUB_USER/citus:11.3.0-alpine
docker push ghcr.io/$GITHUB_USER/citus:11.3.0-alpine
```
