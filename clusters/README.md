# RHACM Assisted Service cluster installation example

## cluster01 cluster example

To instanciate a new cluster:

Copy cluster01 template folder to a new folder.

```
mkdir -p my-new-cluster
cp -r cluster01/* my-new-cluster
```

Change cluster01 references in yaml files to reflect your new cluster name:

```
cd my-new-cluster
sed -i "s/cluster01/my-new-cluster/g" my-new-cluster/kustomization.yaml my-new-cluster/*/*
```

Update the bare metal host resource to reflect your configuration.

```
vi host-inventory/01-bare-metal-host.yaml
```

## All in one creation

To create host environment (infraenv) and cluster at the same time, you can just do:

```
cd my-new-cluster
oc apply -k .
```


## Host environment

You can manage host inventory in an host environment (infraenv) without triggering cluster installation yet.
Host inventory is a long task so it is better to do this in advance to speed up cluster creation.

To do only host inventory:

```
cd my-new-cluster/host-inventory/
oc apply -k .
```


## TIPS

To visualize composed yaml resources before applying them to OpenShift. First you need to install kustomize (from https://kustomize.io/).

Then:

```
kustomize build .
```

In every folder where kustomiation.yaml file exists.

## TODO

Feel free to reach me (phuet@redhat.com) for any question.

