# Helm repository for gopaddle community (lite) edition

This outlines the steps to add this helm repository to do a helm-based
installation of gopaddle community (lite) edition.

The gopaddle community (lite) edition is also referred with the names
gp-lite and/or gopaddle-lite.

## Steps to add gp-lite helm repository
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

## Install gp-lite from its helm repository

Once you have added gp-lite helm repository, you can do a helm install of the
software supplied by this repository in the following steps:

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

## Wait for ready state

Before you can use all the gopaddle services, they need to be in Ready state.
To check and wait until all the services move to Ready state, use the below
command:

$ sudo kubectl wait --for=condition=ready pod -l released-by=gopaddle -n gp-lite

The following is a sample output when the gopaddle services are in ready state:
```
pod/rabbitmq-0 condition met
pod/influxdb-0 condition met
pod/esearch-0 condition met
pod/redis-8564f6b9fd-zqb2q condition met
pod/mongodb-0 condition met
pod/appworker-7b687d86f6-hxp8s condition met
pod/gpcore-6bc47c5c94-kq9jk condition met
pod/costmanager-564c95fcdf-x7f2t condition met
pod/clustermanager-d95cccbc-dhkl9 condition met
pod/deploymentmanager-7967f54468-qw24m condition met
pod/nodechecker-7ddfb5b556-pb9xm condition met
pod/domainmanager-7c6c6f57f7-xfn2j condition met
pod/marketplace-97bfcb68f-lnmnq condition met
pod/configmanager-5c6878bc99-8pzw7 condition met
pod/activitymanager-b7d669fb8-pcnhn condition met
pod/appscanner-677cd5799-ztrxj condition met
pod/usermanager-796bf9c8c9-f8tgg condition met
pod/cloudmanager-6c8dd7c6c5-d8xpg condition met
pod/alertmanager-77d4478976-24pgc condition met
pod/webhook-785c846b44-wxwwd condition met
pod/gateway-b768864ff-s54b2 condition met
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
