# Minikube
## OS: ubuntu 16.xxx
## Server: ec2

1. Install Docker 18.06

Compatible Docker check: https://github.com/kubernetes/kubernetes/blob/master/cmd/kubeadm/app/util/system/docker_validator.go#L41
https://docs.docker.com/install/linux/docker-ce/ubuntu/
```jshelllanguage
sudo apt-get install docker-ce=18.06.1~ce~3-0~ubuntu
```

2. Install kubectl

https://kubernetes.io/docs/tasks/tools/install-kubectl/
```jshelllanguage

sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

3. Install minikube

https://github.com/kubernetes/minikube/releases
```jshelllanguage
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.30.0/minikube-linux-amd64 && chmod +x minikube && sudo cp minikube /usr/local/bin/ && rm minikube
```

4. Start minikube
```jshelllanguage
sudo minikube start --vm-driver=none
```

output
```text
Starting local Kubernetes v1.10.0 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
Kubectl is now configured to use the cluster.
===================
WARNING: IT IS RECOMMENDED NOT TO RUN THE NONE DRIVER ON PERSONAL WORKSTATIONS
	The 'none' driver will run an insecure kubernetes apiserver as root that may leave the host vulnerable to CSRF attacks

When using the none driver, the kubectl config and credentials generated will be root owned and will appear in the root home directory.
You will need to move the files to the appropriate location and then set the correct permissions.  An example of this is below:

	sudo mv /root/.kube $HOME/.kube # this will write over any previous configuration
	sudo chown -R $USER $HOME/.kube
	sudo chgrp -R $USER $HOME/.kube

	sudo mv /root/.minikube $HOME/.minikube # this will write over any previous configuration
	sudo chown -R $USER $HOME/.minikube
	sudo chgrp -R $USER $HOME/.minikube

This can also be done automatically by setting the env var CHANGE_MINIKUBE_NONE_USER=true
Loading cached images from config file.
```

5. Deployment
```jshelllanguage
kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.10 --port=8080
```
6. Get pods
```jshelllanguage
kubectl get pod
```