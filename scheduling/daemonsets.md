1. Deploy a DaemonSet for FluentD Logging.

Use the given specifications.

CheckCompleteIncomplete
Name: elasticsearch

Namespace: kube-system

Image: k8s.gcr.io/fluentd-elasticsearch:1.20

HINT >> An easy way to create a DaemonSet is to first generate a YAML file for a Deployment with the command kubectl create deployment elasticsearch --image=k8s.gcr.io/fluentd-elasticsearch:1.20 -n kube-system --dry-run=client -o yaml > fluentd.yaml. Next, remove the replicas, strategy and status fields from the YAML file using a text editor. Also, change the kind from Deployment to DaemonSet.

Finally, create the Daemonset by running kubectl create -f fluentd.yaml

2. 

3. 

4. 

5. 

6. 

7. 

8. 

9. 

10. 

11. 

