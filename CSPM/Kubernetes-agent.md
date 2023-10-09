## create new cloud instance and install minikube and helm 


```
 sudo apt-get update 
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates InRelease                           
Hit:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports InRelease                         
Hit:4 http://security.ubuntu.com/ubuntu jammy-security InRelease                                       
Hit:5 https://esm.ubuntu.com/apps/ubuntu jammy-apps-security InRelease                                 
Hit:6 https://esm.ubuntu.com/apps/ubuntu jammy-apps-updates InRelease
Hit:7 https://esm.ubuntu.com/infra/ubuntu jammy-infra-security InRelease
Hit:8 https://esm.ubuntu.com/infra/ubuntu jammy-infra-updates InRelease
Reading package lists... Done

 sudo apt install -y curl wget apt-transport-https
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
wget is already the newest version (1.21.2-2ubuntu1).
wget set to manually installed.
The following NEW packages will be installed:
  apt-transport-https
The following packages will be upgraded:
  curl libcurl4
2 upgraded, 1 newly installed, 0 to remove and 110 not upgraded.
Need to get 486 kB of archives.
After this operation, 169 kB of additional disk space will be used.
Get:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 apt-transport-https all 2.4.10 [1510 B]
Get:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 curl amd64 7.81.0-1ubuntu1.13 [194 kB]
Get:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcurl4 amd64 7.81.0-1ubuntu1.13 [290 kB]
Fetched 486 kB in 0s (15.8 MB/s)
Selecting previously unselected package apt-transport-https.
(Reading database ... 64311 files and directories currently installed.)
Preparing to unpack .../apt-transport-https_2.4.10_all.deb ...
Unpacking apt-transport-https (2.4.10) ...
Preparing to unpack .../curl_7.81.0-1ubuntu1.13_amd64.deb ...
Unpacking curl (7.81.0-1ubuntu1.13) over (7.81.0-1ubuntu1.10) ...
Preparing to unpack .../libcurl4_7.81.0-1ubuntu1.13_amd64.deb ...
Unpacking libcurl4:amd64 (7.81.0-1ubuntu1.13) over (7.81.0-1ubuntu1.10) ...
Setting up apt-transport-https (2.4.10) ...
Setting up libcurl4:amd64 (7.81.0-1ubuntu1.13) ...
Setting up curl (7.81.0-1ubuntu1.13) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
Scanning processes...                                                                                                                                                                                                 
Scanning linux images...                                                                                                                                                                                              

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.



```

### install minikube 

```
 curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 82.4M  100 82.4M    0     0  87.8M      0 --:--:-- --:--:-- --:--:-- 87.7M

```

## minikube start 

```
 minikube start 
😄  minikube v1.31.2 on Ubuntu 22.04 (xen/amd64)
👎  Unable to pick a default driver. Here is what was considered, in preference order:
💡  Alternatively you could install one of these drivers:
    ▪ docker: Not installed: exec: "docker": executable file not found in $PATH
    ▪ kvm2: Not installed: exec: "virsh": executable file not found in $PATH
    ▪ podman: Not installed: exec: "podman": executable file not found in $PATH
    ▪ qemu2: Not installed: exec: "qemu-system-x86_64": executable file not found in $PATH
    ▪ virtualbox: Not installed: unable to find VBoxManage in $PATH

❌  Exiting due to DRV_NOT_DETECTED: No possible driver was detected. Try specifying --driver, or see https://minikube.sigs.k8s.io/docs/start/



```

## install docker 

```
 sudo usermod -aG docker $USER && newgrp docker
 sudo apt-get install docker.io
minikube start 
minikube start --driver=docker
```

enforce single core cpus 

```
 minikube start --driver=docker  --extra-config=kubeadm.ignore-preflight-errors=NumCPU --force --cpus=1

```

## verify minikube working or not 

```
minikube kubectl -- get pods -A
    > kubectl.sha256:  64 B / 64 B [-------------------------] 100.00% ? p/s 0s
    > kubectl:  46.98 MiB / 46.98 MiB [-----------] 100.00% 84.12 MiB p/s 800ms
NAMESPACE     NAME                               READY   STATUS    RESTARTS        AGE
kube-system   coredns-5d78c9869d-kgkgc           1/1     Running   0               3m46s
kube-system   etcd-minikube                      1/1     Running   0               4m2s
kube-system   kube-apiserver-minikube            1/1     Running   0               3m59s
kube-system   kube-controller-manager-minikube   1/1     Running   0               4m1s
kube-system   kube-proxy-cmn6s                   1/1     Running   0               3m47s
kube-system   kube-scheduler-minikube            1/1     Running   0               4m1s
kube-system   storage-provisioner                1/1     Running   1 (3m14s ago)   3m55s

```

## install helm 

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 11715  100 11715    0     0   107k      0 --:--:-- --:--:-- --:--:--  107k
Downloading https://get.helm.sh/helm-v3.13.0-linux-amd64.tar.gz
Verifying checksum... Done.
Preparing to install helm into /usr/local/bin
helm installed into /usr/local/bin/helm
```

## add helm repo 

``` 

helm repo add deepfence https://deepfence-helm-charts.s3.amazonaws.com/threatmapper
"deepfence" has been added to your repositories

```

## update repo 

```

helm repo update

```

## install threatmapper 

```

 helm install deepfence-agent deepfence/deepfence-agent   --set managementConsoleUrl=<add-console-ip>   --set deepfenceKey=default:3040db4a-15ef-4de3-a167-40ee186c84e6   --set image.tag=2.0.0   --set image.clusterAgentImageTag=2.0.0   --set clusterName=prod-cluster   --set mountContainerRuntimeSocket.containerdSock=false  --version=2.0.0

  ```

## get visibility kubernetes agent added to deepfence console 
    
![](/images/new-minikube.png)

![](/images/minikube.png)

## scan Minikube kubernetes cluster 

![](/images/minikube-scan.png)


## get NIST compliance report of kubernetes cluster

![](/images/minikube-report.png)



> Threatmapper give more visibility into kubernetes cluster and help to identify threats and vulnerabilities in real time.

