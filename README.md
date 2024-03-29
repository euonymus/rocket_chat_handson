# Kubernetesを使ってRocket Chatを起動するハンズオン

# 参考
[Slide](https://drive.google.com/drive/folders/1tRQtKuMON2Xm_xtRw4PS-wR7VYdetIOV)

## Step1: Namespaceの用意

```bash
$ kubectl config get-contexts
$ kubectl create namespace handson
$ kubectl config set-context handson --namespace=handson --user=docker-desktop --cluster=docker-desktop
$ kubectl config use-context handson
```

## Step2: Check the Cluster

```bash
# Check Cluster
$ kubectl cluster-info

# Check Node
$ kubectl get node
```

## Step3: Run hello-world

```bash
$ kubectl run hello-world --image=hello-world -it --restart=Never


Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

## Step4: Show Pod

```bash
$ kubectl get pod
$ kubectl describe pod
$ kubectl delete pod hello-world
```

## Step5: Pod Practice

```bash
$ kubectl apply -f practices/pod.yml
$ kubectl delete -f practices/pod.yml
```


## Step6: Apply resources

```bash
$ kubectl apply -f k8s/deployment.yml
$ kubectl get deploy
$ kubectl describe deploy NAME
$ kubectl delete -f k8s/deployment.yml

$ kubectl apply -f k8s/service.yml
$ kubectl get service
$ kubectl describe service
$ kubectl get po -l app=web

$ kubectl delete -f k8s/service.yml
```

## Step7: 動作確認

busyboxを使って、対話型の Pod を起動

```bash
$ kubectl run test -it --restart=Never --image=busybox sh
```

```bash
/ # wget -O - http://web-service
```

## Step8: ボリューム

```bash
$ kubectl apply -f k8s/pv.yml
$ kubectl apply -f k8s/pvc.yml
```

## Step9: MongoDB

```bash
$ kubectl apply -f k8s/mongodb.yml
$ kubectl get pod -o wide
$ kubectl get logs POD-NAME
$ kubectl get events
```

```bash
$ kubectl apply -f k8s/svc-mongodb.yml
```

## Step10: Rocket.Chat

[Rocket.Chat](https://hub.docker.com/_/rocket-chat)

```bash
$ kubectl apply -f k8s/deploy-rocket.yml
$ kubectl apply -f k8s/svc-rocket.yml
```


