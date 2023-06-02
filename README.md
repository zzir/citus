improved ZFS performance, pg configure add:

* --with-blocksize=32
* --with-wal-blocksize=64

### codespace build

```
export GITHUB_TOKEN=
export GITHUB_USER=zzir

echo $GITHUB_TOKEN | docker login ghcr.io -u $GITHUB_USER --password-stdin
docker tag citus:11.3.0-alpine ghcr.io/zzir/citus:11.3.0-alpine
docker push ghcr.io/zzir/citus:11.3.0-alpine
```