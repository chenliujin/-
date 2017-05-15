# nsqlookupd
```
$ docker run -d --restart=always --name lookupd -p 4160:4160 -p 4161:4161 nsqio/nsq:v1.0.0-compat /nsqlookupd
```

### Test
```
$ curl x.x.x.x:4161/ping
```

# nsq
```
$ docker run -d --restart=always --name nsqd -v /data/nsqd:/data/nsqd -p 4150:4150 -p 4151:4151 nsqio/nsq:v1.0.0-compat /nsqd --broadcast-address=x.x.x.x --lookupd-tcp-address=x.x.x.x:4160 --data-path=/data/nsqd
```


# nsqadmin
- url: http://x.x.x.x:4171
```
$ docker run -d --restart=always --name nsqadmin -p 4171:4171 nsqio/nsq:v1.0.0-compat /nsqadmin  --lookupd-http-address=x.x.x.x:4161
```


# Topic
```
curl -d 'hello world 1' 'http://x.x.x.x:4151/pub?topic=test'
```


# Channel
一个通道接收到一个话题中所有消息的副本，启用组播方式的传输，使消息同时在每个通道的所有订阅用户间分发，从而实现负载平衡。
```
$ docker run -d --name nsq_to_file1 -v /data/t1:/data/t1 nsqio/nsq:v1.0.0-compat /nsq_to_file --topic=test --channel=t1 --output-dir=/data/t1 --nsqd-tcp-address=x.x.x.x:4150
$ docker run -d --name nsq_to_file2 -v /data/t2:/data/t2 nsqio/nsq:v1.0.0-compat /nsq_to_file --topic=test --channel=t2 --output-dir=/data/t2 --nsqd-tcp-address=x.x.x.x:4150
```


# 参考文献
- [NSQ 官网](http://nsq.io/)
- [GitHub](https://github.com/nsqio/nsq)
- [NSQ的消息订阅发布测试](http://www.cnblogs.com/forrestsun/p/3892710.html)
- [NSQ 指南](http://udn.yyuap.com/doc/wiki/project/nsq-guide/docker.html)
- [NSQ 指南](http://wiki.jikexueyuan.com/project/nsq-guide/internals.html)
- [NSQ：分布式的实时消息平台](http://www.infoq.com/cn/news/2015/02/nsq-distributed-message-platform)
