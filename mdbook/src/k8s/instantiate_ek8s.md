# Instantiate the embedded k8s descriptor via FOrCE

Once the entity have been added, usually, we want to instantiate it. So we can add an instance for a given entity specifying the Cloud in which we want to instantiate it. To instantiate it to a cloud use `-c` (otherwise to connect to a FIM use `-f`.

```sh
fosctl add instance -c 00000000-0000-0000-0000-000000000001 50d97c3c-8930-4d45-85f1-2bd8833bc9db
```

The output returns should be as follows:

```sh
Add(Instance { entity_id: 50d97c3c-8930-4d45-85f1-2bd8833bc9db, fim_id: None, cloud_id: Some(00000000-0000-0000-0000-000000000001) })
69d07b75-0ecd-423c-a069-e6a97804a4c3
```

We can look at the status of this instance, as follows:

```sh
$ fosctl get instance 69d07b75-0ecd-423c-a069-e6a97804a4c3
Get(Instance { id: Some(69d07b75-0ecd-423c-a069-e6a97804a4c3) })
+--------------------------------------+--------------------------------------+---------+-----+--------------------------------------+
| UUID                                 | ID                                   | Status  | FIM | Cloud                                |
+--------------------------------------+--------------------------------------+---------+-----+--------------------------------------+
| 69d07b75-0ecd-423c-a069-e6a97804a4c3 | 50d97c3c-8930-4d45-85f1-2bd8833bc9db | RUNNING |     | 00000000-0000-0000-0000-000000000001 |
+--------------------------------------+--------------------------------------+---------+-----+--------------------------------------+
```

Finally, we can delete and instance as follows:

```sh
fosctl delete instance 69d07b75-0ecd-423c-a069-e6a97804a4c3
```

The output is:

```sh
Delete(Instance { id: 69d07b75-0ecd-423c-a069-e6a97804a4c3 })
```
