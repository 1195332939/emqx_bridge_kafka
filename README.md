The plugin is not perfect, if you are in a hurry, please back to version 3.0, if you are using the official version 4.0, according to the format of the request hook.

# emqx_bridge_kafka

This is a plugin for the EMQX broker that sends all messages received by the broker to kafka.


## Build the EMQX broker

1. Clone emqx-relx project
   We need to clone the EMQX project [GITHUB](https://github.com/emqx/emqx-rel)

    ```shell
      git clone https://github.com/emqx/emqx-rel.git
    ```

2. Open the rebar.config in the 
{deps,
   [{emqx_bridge_kafka, {git, "https://gitbub.com/1195332939/emqx_bridge_kafka.git", {tag, "master"}}},
   ...,
   ]}

3. Add load plugin in relx.config
   >{emqx_kafka_bridge, load},

4. Build

   ```shell
   cd emqx-relx && make
   ```

Configuration

----------------------
You will have to edit the configurations of the bridge to set the kafka Ip address and port.

Edit the file emq-relx/deps/emqx_kafka_bridge/etc/emqx_kafka_bridge.conf

```conf
##--------------------------------------------------------------------
## kafka Bridge
##--------------------------------------------------------------------

## The Kafka loadbalancer node host that bridge is listening on.
##
## Value: 127.0.0.1, localhost
kafka.host = 127.0.0.1

## The kafka loadbalancer node port that bridge is listening on.
##
## Value: Port
kafka.port = 9092

## The kafka loadbalancer node partition strategy.
##
## Value: random, sticky_round_robin, strict_round_robin, custom
kafka.partitionstrategy = random

## Each worker represents a connection to a broker + topic + partition combination.
## You can decide how many workers to start for each partition.
##
## Value:
kafka.partitionworkers = 2

## payload topic.
##
## Value: string
kafka.payloadtopic = Processing

## event topic.
##
## Value: string
kafka.eventtopic = Event

## publish topic.
##
## Value: string
kafka.publishtopic = Publish

## connected topic.
##
## Value: string
kafka.connectedtopic = Connected

## disconnected topic.
##
## Value: string
kafka.disconnectedtopic = Disconnected

## subscribe topic.
##
## Value: string
kafka.subscribetopic = Subscribe

## unsubscribe topic.
##
## Value: string
kafka.unsubscribetopic = Unsubscribe

## delivered topic.
##
## Value: string
kafka.deliveredtopic = Delivered

```

Start the EMQ broker and load the plugin

----------------------

1) cd emqx-relx/_rel/emqx
2) ./bin/emqx start
3) ./bin/emqx_ctl plugins load emqx_kafka_bridge

## License

This project is licensed under the Apache 2.0 License - see the [LICENSE](LICENSE) file for details
