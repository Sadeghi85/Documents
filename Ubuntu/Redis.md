

# Configuring Redis Repo

- Installing redis
```
$ curl https://packages.redis.io/gpg | sudo apt-key add -
$ echo "deb https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
$ apt update
$ apt install redis redis-server
```

- Check Redis version
```
$ apt list -a redis redis-server
or
$ apt-cache policy redis redis-server
```

```
$ systemctl start redis-server
$ systemctl enable redis-server
```