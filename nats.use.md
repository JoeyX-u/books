### run nats-server and enable JetStream
```shell
sudo docker run --net=host  --name nats-server -tid nats:latest -js

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
nats request help.please 'I need help!'
```

>If all subscribers subscribe to the same topic, If all subscribers subscribe to the same topic, one of them will receive the message.
>If the subscriber dies, the message cannot be sent.

### Queue Groups
##### Start the first member of the queue group
```shell
nats reply foo "service instance A Reply# {{Count}}"
```
##### Start the second member of the queue group
```shell
nats reply foo "service instance B Reply# {{Count}}"
```
##### Start the third  member of the queue group
```shell
nats reply foo "service instance C Reply# {{Count}}"
```

##### Publish a NATS message
```shell
nats request foo "Simple request"
```
##### Publish another message
```shell
nats pub foo "Another simple request"
```
>If all subscribers subscribe to the same topic, If all subscribers subscribe to the same topic, one of them will receive the message.
>If the subscriber dies, the message cannot be sent.
