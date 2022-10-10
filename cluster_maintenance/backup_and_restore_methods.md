1. We have a working kubernetes cluster with a set of applications running. Let us first explore the setup.
How many deployments exist in the cluster?

HINT >> Use kubectl get command to check the deployments.
SOLUTION >> Run the kubectl get deployments command


2. What is the `version of ETCD` running on the cluster?
Check the ETCD Pod or Process

HINT >> Look at the ETCD Logs OR check the image used by ETCD pod.

SOLUTION >> 
Look at the ETCD Logs using the command kubectl logs etcd-controlplane -n kube-system or check the image used by the ETCD pod: kubectl describe pod etcd-controlplane -n kube-system
```bash
root@controlplane:~# kubectl -n kube-system logs etcd-controlplane | grep -i 'etcd-version'
"ts":"2022-03-25T08:45:18.872Z","caller":"embed/etcd.go:307","msg":"starting an etcd server","etcd-version":"3.5.1","git-sha":"e8732fb5f"
root@controlplane:~# 
root@controlplane:~# kubectl -n kube-system describe pod etcd-controlplane | grep Image:
    Image:         k8s.gcr.io/etcd:3.5.1-0
root@controlplane:~#
```


3. At what address can you reach the ETCD cluster from the controlplane node?
Check the ETCD Service configuration in the ETCD POD 

HINT >> Use the command kubectl describe pod etcd-controlplane -n kube-system and look for --listen-client-urls

SOLUTION >> 
```
root@controlplane:~# kubectl -n kube-system describe pod etcd-controlplane | grep '\--listen-client-urls'
      --listen-client-urls=https://127.0.0.1:2379,https://10.2.43.11:2379
root@controlplane:~#
```
This means that ETCD is reachable on localhost (127.0.0.1) at port 2379.



4. Where is the ETCD server certificate file located?
Note this path down as you will need to use it later

- /etc/kubernetes/pki/etcd/peer.crt
- /etc/kubernetes/pki/server.crt
- /etc/kubernetes/pki/etcd/server.crt
- /etc/kubernetes/pki/etcd/ca.crt

for myself >> 
```bash
k describe pods etcd-controlplane -n kube-system
# check some words which are related with "the certificate file" on the output
```

HINT >> Check the ETCD pod configuration `kubectl describe pod etcd-controlplane -n kube-system`
SOLUTION >> 
Check the ETCD pod configuration with the command: `kubectl describe pod etcd-controlplane -n kube-system` and look for the value for --cert-file:
```bash
root@controlplane:~# kubectl -n kube-system describe pod etcd-controlplane | grep '\--cert-file'
      --cert-file=/etc/kubernetes/pki/etcd/server.crt
root@controlplane:~#
```

5. Where is the ETCD CA Certificate file located?
Note this path down as you will need to use it later.

- /etc/kubernetes/pki/ca.crt
- /etc/kubernetes/pki/etcd/ca.crt
- /etc/kubernetes/pki/etcd/peer.crt
- /etc/kubernetes/pki/etcd/ca.key

FOR MYSELF >> 
there are some commands options that make me cofuse abou this question 
CA Certificate file?
I can see two ca.crt file. 
5.1) one is --peer-trusted-ca-file : Trusted certificate authority.
5.2) the other is --trusted-ca-file : Trusted certificate authority.
let's google it what it is


HINT >> 

Use the `etcdctl snapshot save` command. You will have to make use of additional flags to connect to the ETCD server. 

`--endpoints` : Optional Flag, points to the address where ETCD is running (127.0.0.1:2379)

`--cacert` : Mandatory Flag (Absolute Path to the CA certificate file)

`--cert` :  Mandatory Flag (Absolute Path to the Server certificate file)

`--key` : Mandatory Flag (Absolute Path to the Key file)

SOLUTION >> 

Run the command:

```bash
root@controlplane:~# ETCDCTL_API=3 etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db

Snapshot saved at /opt/snapshot-pre-boot.db
root@controlplane:~#

```

You may also refer the solution [here](https://github.com/mmumshad/kubernetes-the-hard-way/blob/master/practice-questions-answers/cluster-maintenance/backup-etcd/etcd-backup-and-restore.md)

6. The master node in our cluster is planned for a regular maintenance reboot tonight. While we do not anticipate anything to go wrong, we are required to take the necessary backups. Take a snapshot of the **ETCD** database using the built-in **snapshot** functionality.

Store the backup file at location `/opt/snapshot-pre-boot.db`

- Backup ETCD to /opt/snapshot-pre-boot.db

FOR MYSELF >> should know how to store etcd using kubectl command 

HINT >> 

Use the `etcdctl snapshot save` command. You will have to make use of additional flags to connect to the ETCD server. 

`--endpoints` : Optional Flag, points to the address where ETCD is running (127.0.0.1:2379)

`--cacert` : Mandatory Flag (Absolute Path to the CA certificate file)

`--cert` :  Mandatory Flag (Absolute Path to the Server certificate file)

`--key` : Mandatory Flag (Absolute Path to the Key file)

SOLUTION >> 

Run the command:

```bash
root@controlplane:~# ETCDCTL_API=3 etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db

Snapshot saved at /opt/snapshot-pre-boot.db
root@controlplane:~#

```

You may also refer the solution [here](https://github.com/mmumshad/kubernetes-the-hard-way/blob/master/practice-questions-answers/cluster-maintenance/backup-etcd/etcd-backup-and-restore.md)

7. Great! Let us now wait for the maintenance window to finish. Go get some sleep. (Don't go for real)

Click `Ok` to Continue

**Ok**

---

8. 모든게 잘 됬는데 접속이 안된다네

SOLUTION >> default로 올라온게 아무것도 없음

9. Luckily we took a backup. Restore the original state of the cluster using the backup file.

- Deployments: 2
- Services: 3

HINT >> 

Restore the etcd to a new directory from the snapshot by using the `etcdctl snapshot restore`
 command. Once the directory is restored, update the ETCD configuration to use the restored directory.

SOLUTION >> 

**First Restore the snapshot:**

```
root@controlplane:~# ETCDCTL_API=3 etcdctl  --data-dir /var/lib/etcd-from-backup \
snapshot restore /opt/snapshot-pre-boot.db

2022-03-25 09:19:27.175043 I | mvcc: restore compact to 2552
2022-03-25 09:19:27.266709 I | etcdserver/membership: added member 8e9e05c52164694d [http://localhost:2380] to cluster cdf818194e3a8c32
root@controlplane:~#

```

Note: In this case, we are restoring the snapshot to a different directory but in the same server where we took the backup **(the controlplane node)** As a result, the only required option for the restore command is the `--data-dir`.

Next, update the `/etc/kubernetes/manifests/etcd.yaml`:

We have now restored the etcd snapshot to a new path on the controlplane - `/var/lib/etcd-from-backup`, so, the only change to be made in the YAML file, is to change the hostPath for the volume called `etcd-data` from old directory (`/var/lib/etcd`) to the new directory (`/var/lib/etcd-from-backup`).

```yaml
  volumes:
  - hostPath:
      path: /var/lib/etcd-from-backup
      type: DirectoryOrCreate
    name: etcd-data

```

With this change, `/var/lib/etcd` on the container points to `/var/lib/etcd-from-backup` on the `controlplane` (which is what we want).

When this file is updated, the `ETCD` pod is automatically re-created as this is a static pod placed under the `/etc/kubernetes/manifests` directory.

> Note 1: As the ETCD pod has changed it will automatically restart, and also kube-controller-manager and kube-scheduler. Wait 1-2 to mins for this pods to restart. You can run the command: watch "crictl ps | grep etcd" to see when the ETCD pod is restarted.
> 
> 
> Note 2: If the etcd pod is not getting `Ready 1/1`, then restart it by `kubectl delete pod -n kube-system etcd-controlplane` and wait 1 minute.
> 
> Note 3: This is the simplest way to make sure that ETCD uses the restored data after the ETCD pod is recreated. You **don't** have to change anything else.
> 

If you do change `--data-dir` to `/var/lib/etcd-from-backup` in the ETCD YAML file, make sure that the `volumeMounts` for `etcd-data` is updated as well, with the mountPath pointing to `/var/lib/etcd-from-backup` **(THIS COMPLETE STEP IS OPTIONAL AND NEED NOT BE DONE FOR COMPLETING THE RESTORE)**