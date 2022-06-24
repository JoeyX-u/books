### run nats-server
```shell
sudo docker run --net=host  --name nats-server -tid nats:latest

```
### Pub/Sub Walkthrough
##### create a subscriber
```shell
nats sub 'msg.test'
```
```shell
nats sub 'msg.test.*'
```
```shell
nats sub 'msg.test.>'
```
```shell
nats sub 'msg.*.hello.>'
```

##### create a publisher  
```shell
nats pub msg.test hello
```
```shell
nats pub msg.test.hello hello
```
```shell
nats pub msg.test.hello.world hello
```
```shell
nats pub msg.test.hello.world.one hello
```

>If all subscribers subscribe to the same topic, they will receive the message.
>If the subscriber dies,the message will disappear.


### Request-Reply Walkthrough
##### run the reply client listener
```shell
nats reply help.please 'OK, I CAN HELP!!!'
```

##### run the request client
```shell
nats reply help.please 'OK, I CAN HELP!!!'
```

>If all subscribers subscribe to the same topic, If all subscribers subscribe to the same topic, one of them will receive the message.
>If the subscriber dies, the message cannot be sent.
