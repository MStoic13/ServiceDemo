# Setup

- DONE make repo
- DONE install Go
    > * installed golang from the Linux Mint software manager
- DONE make a hello world Go app
    > * followed this tutorial https://go.dev/doc/tutorial/getting-started
    
    > * included go.sum and go.mod files in the repo as per go wiki https://go.dev/wiki/Modules#should-i-commit-my-gosum-file-as-well-as-my-gomod-file
- DONE install K8
    > * followed this guide https://kubernetes.io/docs/setup/
    > * installed `kubectl` using Debian native pkg mgr using this guide https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management
    > * installed `kvm` which is virtualization for Linux. I used this guide first https://docs.docker.com/desktop/setup/install/linux/#kvm-virtualization-support, then this guide https://minikube.sigs.k8s.io/docs/drivers/kvm2/ and then this guide https://wiki.debian.org/KVM#Installation.
    > * installed `minikube` using this guide https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download and it failed to start right after installation due to permissions errors but it worked after restarting the computer. My user was already added to kvm. I chose `minikube` because it was a faster setup than docker and I wanted to get something quick going to learn. I saw that kvm is a prerequisite for Docker so when I do install Docker I will already have half the setup.
    > I can now see all interfaces with the bellow command. default is the default libvirt network and mk-minikube is a network created for default minikube profile.
    > ```
    > $ sudo virsh net-list --all
    > Name          State    Autostart   Persistent
    > ------------------------------------------------
    > default       active   yes         yes
    > mk-minikube   active   yes         yes
    > ```
    > Now I can see my cluster using `kubectl`
    > ```
    > $ kubectl get po -A
    > NAMESPACE     NAME                               READY   STATUS    RESTARTS        AGE
    > kube-system   coredns-7d764666f9-nlk5v           1/1     Running   0               7m8s
    > kube-system   etcd-minikube                      1/1     Running   0               7m14s
    > kube-system   kube-apiserver-minikube            1/1     Running   0               7m14s
    > kube-system   kube-controller-manager-minikube   1/1     Running   0               7m14s
    > kube-system   kube-proxy-rlwft                   1/1     Running   0               7m9s
    > kube-system   kube-scheduler-minikube            1/1     Running   0               7m15s
    > kube-system   storage-provisioner                1/1     Running   1 (6m37s ago)   7m12s
    > ```
    > I enabled the metrics-server addon and started the dashboard which is a local web page with metrics for my cluster. It is empty now because I didn't deploy anything.
    > ```
    > $ minikube addons enable metrics-server
    > $ minikube dashboard
    > ```
- deploy my hello world Go app to my local K8

