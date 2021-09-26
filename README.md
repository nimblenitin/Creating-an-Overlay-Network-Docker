# Creating-an-Overlay-Network-Docker

The overlay network driver creates a distributed network among multiple Docker daemon hosts. This network sits on top of (overlays) the host-specific networks, allowing containers connected to it (including swarm service containers) to communicate securely when encryption is enabled.

Steps to create an Overlay network-

```

1. On the master, list all the networks and check the Driver type of swarm cluster 
$ sudo docker network ls

2. On worker node, list all the networks and check the Driver type of swarm cluster
$ sudo docker network ls

3. Create an overlay network and run a replicated service on it
$ sudo docker network create -d overlay nginx-net1
$ sudo docker service create --name nginx-service1 \
> --publish target=80,published=80 --replicas=5 \
> --network nginx-net1 nginx

4. List all the service tasks created by the replicated service
$ sudo docker service ls

5. Inspect the nginx-net1 network on manager node and check the Containers section for the service tasks connected to the overlay network from this host
$ sudo docker network inspect nginx-net1

6. Inspect the nginx-net1 network on worker node and check the Containers section for the service tasks connected to the overlay network from this host.
$ sudo docker network inspect nginx-net1

7. On the manager node, inspect the replicated service and check the Ports under the Endpoints section
$ sudo docker service inspect nginx-service1

8. Run the following command on manager node to clean the replicated service and network:
$ sudo docker service rm nginx-service1
$ sudo docker network rm nginx-net1

```
