# Helm repository for gopaddle community (lite) edition

This outlines the steps to add this helm repository to do a helm-based
installation of gopaddle community (lite) edition.

The gopaddle community (lite) edition is also referred with the names
gp-lite and/or gopaddle-lite.

## step to add gp-lite helm repository
```
$ sudo helm repo add gp-lite https://gopaddle-io.github.io/gopaddle-lite
```

To confirm that the above has succeeded, issue the following command:
```
$ sudo helm repo update
```

You'll see output like the following:
```
...Successfully got an update from the "gp-lite" chart repository
Update Complete. ⎈Happy Helming!⎈
```

Once the above is done, you can do a helm install of the software supplied
by this repository in the following steps:

#### Note: The below steps assume gp-lite version 4.2.3. If you are installing a different version number, substitute this with the corresponding version number.

1. Create a namespace for gp-lite:

```
$ sudo kubectl create ns gp-lite
```

2. Install rabbitmq:

```
$ sudo helm install gp-rabbitmq-4-2 gp-lite/gp-lite --namespace gp-lite --set global.routingType=NodePortWithOutIngress --set global.installType=public --set global.storageClassName=microk8s-hostpath --set global.gp-rabbitmq.enabled=true --set global.gp-lite-core.enabled=false --version 4.2.3
```

#### Note: gopaddle installer requires storage configuration (StorageClass) in the Kubernetes environment in order to provision gopaddle services.

The storageClassName can either be specified as above for "microk8s-hostpath", or, if you want to use a different StorageClass, obtain that by the command:
```
$ sudo kubectl get sc
```

A sample output is shown below:
```
$ sudo kubectl get sc
NAME                          PROVISIONER            RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
microk8s-hostpath (default)   microk8s.io/hostpath   Delete          Immediate           false                  76m
```

3. Install gp-lite:

```
$ sudo helm install gp-core-4-2 gp-lite/gp-lite  --namespace gp-lite  --set global.routingType=NodePortWithOutIngress --set global.installType=public --set global.storageClassName=microk8s-hostpath --set global.cluster.provider=other --set-string global.gopaddle.https=false --set-string global.gopaddleWebhook.https=false --set global.staticIP=$STATICIP  --set global.gp-rabbitmq.enabled=false --set global.gp-lite-core.enabled=true --set gateway.gpkubeux.installSource=microk8s --version 4.2.3
```

## microk8s addon for gopaddle community (lite) edition

The microk8s addon for gopaddle community (lite) edition uses this helm
repository for helm-based installation of gopaddle-lite.

The general documentation for microk8s addons is at:
https://github.com/canonical/microk8s-community-addons  
The same is also available from:
https://github.com/gopaddle-io/microk8s-community-addons
  
For documentation specific to microk8s addon for gopaddle community (lite)
edition, see:
https://github.com/gopaddle-io/microk8s-community-addons/blob/main/README.gopaddle_addon.md

## Help

For help related to gopaddle community (lite) edition, visit the gopaddle Help Center at:
     https://help.gopaddle.io
