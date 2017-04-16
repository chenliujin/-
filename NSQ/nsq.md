# nsqlookupd
```
$ docker run -d --name lookupd -p 4160:4160 -p 4161:4161 nsqio/nsq:v1.0.0-compat /nsqlookupd
```

### Test
```
$ curl 127.0.0.1:4161/ping
```

# nsq
```
$ docker run -d --name nsqd -v /data/nsqd:/data/nsqd -p 4150:4150 -p 4151:4151 nsqio/nsq:v1.0.0-compat /nsqd --broadcast-address=127.0.0.1  --lookupd-tcp-address=127.0.0.1:4160 --data-path=/data/nsqd
```

### Test
```
curl -d 'hello world 1' 'http://127.0.0.1:4151/pub?topic=test'
```


# nsqadmin
- url: http://127.0.0.1:4171
```
$ docker run -d --name nsqadmin -p 4171:4171 nsqio/nsq:v1.0.0-compat /nsqadmin  --lookupd-http-address=127.0.0.1:4161
```


# Channel
```
$ docker run -d --name nsq_to_file1 -v /data/t1:/data/t1 nsqio/nsq:v1.0.0-compat /nsq_to_file --topic=test --channel=t1 --output-dir=/data/t1 --nsqd-tcp-address=127.0.0.1:4150
$ docker run -d --name nsq_to_file2 -v /data/t2:/data/t2 nsqio/nsq:v1.0.0-compat /nsq_to_file --topic=test --channel=t2 --output-dir=/data/t2 --nsqd-tcp-address=127.0.0.1:4150
```


# 参考文献
- [NSQ 官网](http://nsq.io/)
- [NSQ的消息订阅发布测试](http://www.cnblogs.com/forrestsun/p/3892710.html)
- [NSQ 指南](http://udn.yyuap.com/doc/wiki/project/nsq-guide/docker.html)
