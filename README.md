# trash-bin
Collect normal stuffs, or something is weird, or maybe nothing


#### Kafka - Zookeeper

**1. New consumer uses `--bootstrap-server <kafka>` not working, but old style `--zookeeper <zk>` works -> Fix: remove /brokers from `zookeeper` container**
? How to do that
- Stop and remove `kafka` container: docker stop <kafka_container_name> | docker rm <kafka_container_name>
- Enter `zookeeper` container: docker exec -it <zk_c_n> su
- Run: `find / -name 'zkCli.sh'`
- Go to the zoo: `./zkCli.sh`
- Some useful commands that you probably use in the zoo:
    
    + help
    + `path` presents location of secret folders, should start with `path=/`
    + `ls /brokers` -> `ls /brokers/ids` -> `ls /brokers/topics`
    + `rmr /brokers` to remove all brokers <- this step that we need to do in order to resolve problem
- Start `kafka` container again
- Enter `kafka` container and check by command below:
```bash
# kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my_topic --from-beginning
```
