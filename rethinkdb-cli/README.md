# RethinkDB CLI

## Build
```
docker build -t rethinkdb-cli .
```

## Restore

```
docker run -v /path/to/dump.tar.gz:/dump.tar.gz --network=localhost rethinkdb-cli restore /dump.tar.gz [options]
```
