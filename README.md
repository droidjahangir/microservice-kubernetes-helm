microservice demo app github repository link : https://github.com/GoogleCloudPlatform/microservices-demo

# Install these following tools

1. Install minikube with this command
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
minikube is required for building kubernetes cluster in local development. because in single machine minikube manage master node and worker node.

Official guide : https://minikube.sigs.k8s.io/docs/start/

**start minikube with docker using this command**
```
minikube start --driver=docker
```

2. Install kubectl from official documentation :
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

Maybe we don't need to install kubectl because kubectl is dependency of minikube.

3. Install docker/kvm2 for driver hypervisor
after installing docker we need to create an user for docker driver
```
sudo usermod -aG docker $USER && newgrp docker
minikube start --driver=docker
```

4. Install helm
Official helm github release link : 
https://github.com/helm/helm/releases

from this link we need to download binary file like `helm-v3.12.3-linux-amd64.tar.gz`

untar this compressed file
```
tar xvf helm-v3.12.3-linux-amd64.tar.gz
```
then move to binary folder
```
sudo mv linux-amd64/helm /usr/local/bin
```
then check the version `helm version`

5. Install helmfile
Download helmfile from Official release : `https://github.com/helmfile/helmfile/releases` 
download linux binary `helmfile_0.156.0_linux_amd64.tar.gz`

untar this compressed file
```
tar xvf helmfile_0.156.0_linux_amd64.tar.gz
```
then move to binary folder
```
sudo mv helmfile /usr/local/bin
```
then check the version `helmfile version`


```
helmfile sync/apply
helmfile destroy
```

# Create helm project
```
helm create microservice
```

make executable file for `install.sh` and `uninstall.sh`
```bash
chmod u+x install.sh
chmod u+x uninstall.sh
```

# Run helm project
2 ways to run this project :
first is `helmfile sync` 
another is: `./install.sh`

**helmfile documentation : `https://helmfile.readthedocs.io/en/latest/`**

then access this frontend app service, first we need to find cluster ip address
```
minikube ip
```
then find nodeport for frontend service

```
kubectl describe service frontend
```

after finding port enter this url like me
```
http://192.168.49.2:30422
```

# Uninstall all of kubectl components
```
./uninstall
```