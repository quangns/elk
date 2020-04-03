## start docker-compose
# docker-compose logstash không có build
```
docker-compose -f elk-compose.yml up --force-recreate -d
```

# docker-compose logstash có build
```
docker-compose -f elk-compose.yml up --force-recreate -d rebuild
```

## stop docker-compose
```
docker-compose down
```
