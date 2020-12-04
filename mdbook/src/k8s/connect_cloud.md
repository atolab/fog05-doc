# Connect Eclipse fog05 FOrcE with K8s cluster cloud

The first thing we need to do is to add a Cloud site, which is a Kubernetes cluster. Let us do this:

```bash
 fosctl add cloud 00000000-0000-0000-0000-000000000001 k8s/config k8s/ca k8s/cert k8s/key
 ```
In the previous command, we needed to pass:
- The cloud UUID
- The K8s configuration
- The K8s CA file
- The K8s Cert file, and
- The K8s Key file
In order to be able to authenticate with the Kubernetes' Cluster

The output should be:

```bash
Add(Cloud { cloud_id: 00000000-0000-0000-0000-000000000001, cloud_conf_path: "k8s/config", cloud_ca: "k8s/ca", cloud_cert: "k8s/cert", cloud_key: "k8s/key" })
00000000-0000-0000-0000-000000000001
```

To test it, we can run:

```bash
 fosctl get cloud
```

The output should be:

```bash
Get(Cloud { id: None })
+--------------------------------------+
| UUID                                 |
+--------------------------------------+
| 00000000-0000-0000-0000-000000000001 |
+--------------------------------------+
```
