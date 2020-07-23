# Installing K8s cluster in minutes

![k8s](https://raw.githubusercontent.com/rahulwaykos/kubernetes/master/k01/kubernetes.png)

The process of creating a cluster is bit hectic. It is easy but time consuming. You have to follow the lots of steps to get kubernetes cluster up running. There are kubernetes playground available online to play with and practice your skills. But if you are planning to set up on in-house or on cloud environment for testing of practising you skills, then this blog is for you. I am not going to describe each every step to create cluster. Although this blog follow official docs of kubernetes to create cluster.

It is mandatory to meet hardware requirements to set up cluster. 
- Minimal required memory & CPU (cores)
    1. Master node’s minimal required memory is 2GB and the worker node needs minimum is 1GB
    2. The master node needs at least 1.5 and the worker node need at least 0.7 cores.

If you fullfil these, you are ready to go. Just run following command and enter IP address of master(for API server) when prompted.

```
$ curl https://raw.githubusercontent.com/rahulwaykos/k8s/master/install.sh | sh
```
Wait for process to end. Copy all the files from k8s/nodes directory to respective worker nodes to join the cluster.

```
$ scp k8s/nodes/* root@<worker_node_ip>:~
```
After copying all files switch to respective node and run following command:

```
$ sh node_join.sh
```

And your are good to go !!!

Switch to kubernetes master and check whether your cluster is up and running. If not wait for few minutes to run all pods.

Note: If you happens to reboot the machine remember to run the swapoff -a command after every reboot. As above script does changes your fstab entry to disable swap. 

Hope you like this blog!!! Please suggest any changes required or any errors occured during the setup to update the script. Thanks!!!!
