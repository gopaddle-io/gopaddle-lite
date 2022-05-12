# Helm repository for gopaddle community (lite) edition

This outlines the steps to add this helm repository to do a helm install of
gopaddle community (lite) edition.

The gopaddle community (lite) edition is also referred with the names
gp-lite and/or gopaddle-lite.

## step to add gp-lite helm repository
```
sudo helm repo add gp-lite https://gopaddle-io.github.io/gopaddle-lite
```

To confirm that the above has succeeded, issue the following command:
```
sudo helm repo update
```

You'll see output like the following:
```
...Successfully got an update from the "gp-lite" chart repository
Update Complete. ⎈Happy Helming!⎈
```

Once the above is done, you can do a helm install of the software supplied
by this repository.

Example:
```
```

## microk8s addon for gopaddle community (lite) edition:

This general documentation for microk8s addons is at:
https://github.com/canonical/microk8s-community-addons
  
The same is also available from:
https://github.com/gopaddle-io/microk8s-community-addons
  
For documentation specific to mircok8s addon for
gopaddle community (lite) edition, see:
https://github.com/gopaddle-io/microk8s-community-addons/blob/main/README.gopaddle_addon.md

## Help:

```
gopaddle lite is a community edition of gopaddle.
For help related to this, visit the gopaddle Help Center at:
     https://help.gopaddle.io
```
