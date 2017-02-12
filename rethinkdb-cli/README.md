# RethinkDB CLI

## Build
```
docker build -t rethinkdb-cli .
```

## Restore

```
docker run -v /path/to/dump.tar.gz:/dump.tar.gz --network=host rethinkdb-cli rethinkdb restore /dump.tar.gz [options]
```
