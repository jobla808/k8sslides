## Day 3 Bis

---

## How to Setup a 3 Zones cluster in a single Region

---

## Install kops and kubectl

https://github.com/kubernetes/kops/blob/master/docs/install.md

---

## Install gcloud sdk

https://cloud.google.com/sdk/downloads

--- 

## Login with your GCP account 

--- 

## Download the default account json file for GCP

---

### Place the json file in a safe place. And create the required variable.

```bash
chmod 600 myaccount.json
mv myaccount.json /somewhere/safe/
export GOOGLE_APPLICATION_CREDENTIALS=/somewhere/safe/myaccount.json
```

---

## Create a bucket for storing configuration

```bash
gsutil mb gs://kubernetes-clusters-whatever/
```

---

### Set environment Variables
```bash
export PROJECT=`gcloud config get-value project`
export KOPS_FEATURE_FLAGS=AlphaAllowGCE # to unlock the GCE features
```

---

## Create the cluster

```bash
kops create cluster  --state=gs://kubernetes-cluster-whatever/ \
--node-count 3 --zones us-west1-a,us-west1-b,us-west1-c     \
--master-zones us-west1-b,us-west1-c,us-west1-a   --node-size n1-standard-2 \
--master-size g1-small     --topology private     --networking kopeio-vxlan \
--cloud=gce mycluster.k8s.local --yes
```
--- 

### Now you have all the concepts and experience to find and fix issues.

---

## Exercise

1. Check if you can access the cluster using kubectl.  If not, find out why, and fix it.
1. Can you see the nodes on the cluster?  If not, find out why.
1. Run kubectl to create a pod or a deployment.  Check the result.
1. If there are issues with the cluster, without using google, find the answer to the problem.
1. Validate and Delete the cluster using kops.

---

## Thank you
