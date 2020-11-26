# fosctl usage

Use of `fosctl` is quite easy, you have three base commands `add`, `get` and `delete` that applies to different kind of resources:

- fim
- cloud
- entity
- instance

The help can be issued by `fosctl -h` and it provides information for each command and each resource.

Let's add a new FIM to our orchestation engine.

```bash
fosctl add fim 00000000-0000-0000-0000-000000000000 tcp/192.168.122.206:7447
Add(FIM { fim_id: 00000000-0000-0000-0000-000000000000, locator: "tcp/192.168.122.206:7447" })
00000000-0000-0000-0000-000000000000
```

## FIM Operations

We need to pass the `UUIDv4` of the `FIM` we want to add (it is used to identify the FIM by the orchestartor) and the locator to access the Zenoh of that FIM

We can also list the available FIMs, as follows:

```bash
 fosctl get fim
Get(FIM { id: None })
+--------------------------------------+
| UUID                                 |
+--------------------------------------+
| 00000000-0000-0000-0000-000000000000 |
+--------------------------------------+
```

Additionaly, we can ask to print more detailed information about a specific FIM

```bash
$ fosctl get fim 00000000-0000-0000-0000-000000000000
Get(FIM { id: Some(00000000-0000-0000-0000-000000000000) })
+--------------------------------------+--------------------------+
| UUID                                 | Locator                  |
+--------------------------------------+--------------------------+
| 00000000-0000-0000-0000-000000000000 | tcp/192.168.122.206:7447 |
+--------------------------------------+--------------------------+
```

Finally, we can remove a FIM as follows:

```bash
$ fosctl delete fim 00000000-0000-0000-0000-000000000000
Delete(FIM { id: Some(00000000-0000-0000-0000-000000000000) })
00000000-0000-0000-0000-000000000000
```


## Cloud Operations

We can also add a Cloud site, which is a Kubernetes cluster, let's do this:

```bash
fosctl add cloud 00000000-0000-0000-0000-000000000001 k8s/config k8s/ca k8s/cert k8s/key
Add(Cloud { cloud_id: 00000000-0000-0000-0000-000000000001, cloud_conf_path: "k8s/config", cloud_ca: "k8s/ca", cloud_cert: "k8s/cert", cloud_key: "k8s/key" })
00000000-0000-0000-0000-000000000001
```

In this case we need to pass the cloud UUID, the K8s configuration file along with the CA, Cert and Key file in order to be able to authenticate with the Cluster

Additionaly, we can list the clouds as follows:

```bash
$ fosctl get cloud
Get(Cloud { id: None })
+--------------------------------------+
| UUID                                 |
+--------------------------------------+
| 00000000-0000-0000-0000-000000000001 |
+--------------------------------------+
```

Finally, we remove a cloud as follows:


```bash
$ fosctl delete cloud 00000000-0000-0000-0000-000000000001
Delete(Cloud { id: Some(00000000-0000-0000-0000-000000000001) })
00000000-0000-0000-0000-000000000001
```


## Entity Operations

We can add an new entity to the catalog, as folows:

```bash
fosctl add entity entity.json

Add(Entity { descriptor_path: "fosctl/examples/entity.json" })
3c02af14-5826-449f-bfaa-9a8dd54d04ff
```

Also, we can list the available entities:

```bash
fosctl get entity
Get(Entity { id: None })
+--------------------------------------+----------------+
| Entity UUID                          | ID             |
+--------------------------------------+----------------+
| 3c02af14-5826-449f-bfaa-9a8dd54d04ff | example-entity |
+--------------------------------------+----------------+
```

Additionally, can ask for detailed information about an entity:

```bash
fosctl get entity 3c02af14-5826-449f-bfaa-9a8dd54d04ff
Get(Entity { id: Some(3c02af14-5826-449f-bfaa-9a8dd54d04ff) })
+--------------------------------------+----------------+-----------------------+---------+
| UUID                                 | ID             | Name                  | Version |
+--------------------------------------+----------------+-----------------------+---------+
| 3c02af14-5826-449f-bfaa-9a8dd54d04ff | example-entity | example simple entity | 0.0.1   |
+--------------------------------------+----------------+-----------------------+---------+
FDUs:
+--------------------------------------+------------------+-----------------+---------+------------+-----------+
| UUID                                 | ID               | Name            | Version | Hypervisor | Depend On |
+--------------------------------------+------------------+-----------------+---------+------------+-----------+
| 88299c6a-8ced-4292-804d-3454c161b3c1 | nginx-docker-fdu | nginx component | 0.0.1   | LXD        | []        |
+--------------------------------------+------------------+-----------------+---------+------------+-----------+
Networks:
+-------+-----------+------------+
| ID    | Link Kind | IP Version |
+-------+-----------+------------+
| vld-1 | L2        | IPV4       |
+-------+-----------+------------+
```


Finally, we can remove the entity from the catalog, as follows:

```bash
fosctl delete entity 3c02af14-5826-449f-bfaa-9a8dd54d04ff

Delete(Entity { id: 3c02af14-5826-449f-bfaa-9a8dd54d04ff })
3c02af14-5826-449f-bfaa-9a8dd54d04ff
```

More examples can be found [here](https://github.com/eclipse-fog05/fog05/tree/0.2.x/src/utils/fosctl/examples)


## Instance operations

Once we have added an entity we usually want to instantiate it. So we can add an instance for a given entity specifing the FIM and/or Cloud in which we want to instantiate it.

```bash
fosctl add instance -f 00000000-0000-0000-0000-000000000000 54435d55-ba1f-408e-99ac-f8209d79c7ef
Add(Instance { entity_id: 54435d55-ba1f-408e-99ac-f8209d79c7ef, fim_id: Some(00000000-0000-0000-0000-000000000000), cloud_id: None })
dfb3b37e-0036-4778-8e1d-12bbb37a1570
```

In this case we are just specifing the FIM where to instantiate, the cloud will be passed using the -c flag.

We can look at the status of this instance, as follows:

```bash
fosctl get instance dfb3b37e-0036-4778-8e1d-12bbb37a1570
Get(Instance { id: Some(dfb3b37e-0036-4778-8e1d-12bbb37a1570) })
+--------------------------------------+--------------------------------------+---------+--------------------------------------+-------+
| UUID                                 | ID                                   | Status  | FIM                                  | Cloud |
+--------------------------------------+--------------------------------------+---------+--------------------------------------+-------+
| dfb3b37e-0036-4778-8e1d-12bbb37a1570 | 54435d55-ba1f-408e-99ac-f8209d79c7ef | RUNNING | 00000000-0000-0000-0000-000000000000 |       |
+--------------------------------------+--------------------------------------+---------+--------------------------------------+-------+
```

Finally, we can delete and instance as follows:

```bash
fosctl delete instance dfb3b37e-0036-4778-8e1d-12bbb37a1570
Delete(Instance { id: dfb3b37e-0036-4778-8e1d-12bbb37a1570 })
dfb3b37e-0036-4778-8e1d-12bbb37a1570

```


