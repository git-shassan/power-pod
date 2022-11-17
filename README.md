A simple pod that runs as a job inside a cluster using privilaged service account. This can be used to execute various OC commands as part of an automated process... 

== Running the POD:
```
shassan@SM-1 power_pod % oc apply -k ./power-pod 
serviceaccount/cli-job-sa created
clusterrolebinding.rbac.authorization.k8s.io/cli-job-sa-testing-rolebinding created
job.batch/testjob created
shassan@SM-1 power_pod % oc get all -n my-namespace
NAME                READY   STATUS    RESTARTS   AGE
pod/testjob-dp2pr   1/1     Running   0          17s

NAME                COMPLETIONS   DURATION   AGE
job.batch/testjob   0/1           17s        17s
```
== Connecting to the POD:
```
shassan@SM-1 power_pod % oc exec -it testjob-dp2pr -n my-namespace -- /bin/bash
```
== Now from witnin the POD:
```
[root@testjob-dp2pr /]# oc get nodes
NAME      STATUS                     ROLES           AGE   VERSION
master1   Ready                      master,worker   87d   v1.23.5+012e945
master2   Ready                      master,worker   87d   v1.23.5+012e945
master3   Ready                      master,worker   87d   v1.23.5+012e945
worker1   Ready,SchedulingDisabled   worker          87d   v1.23.5+012e945
worker2   Ready                      worker          87d   v1.23.5+012e945
[root@testjob-dp2pr /]#
```
