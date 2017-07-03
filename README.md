# PGAdmin
This is a single Helm chart that deploys a pgAdmin instance to your Kubernetes cluster.

## Prerequisites
This install assumes you have an existing Kubernetes cluster installed and a [postgresql](https://github.com/kubernetes/charts/tree/master/stable/postgresql) instance deployed.

## Package
Once you've cloned this repo, you can create your helm package by running the following command in the repo's root directory:
```
helm package .
```

## Install
After packaging the chart, you then install it into your Kubernetes cluster by targeting the packaged archive:
```
helm install pgadmin-0.1.0.tgz
```
Optionally, you can provide a custom username and password:
```
helm install --set pgadmin.username=myuser,pgadmin.password=mypassword pgadmin-0.1.0.tgz
```
The deployment will take a while to provision a public IP for the service. You can watch for this using the following command:
```
kubectl get svc -w -l app=pgadmin
```

## Configure
When the deployment has finished and you have an external IP for your pgAdmin service, you can go to the pgAdmin portal at `http://{external-ip}:5050/`.

**Default Credentials:** \
*username:* pgadmin4@pgadmin.org \
*password:* admin

Once logged in, add a new server and provide the Cluster IP, username and password for your postgres service.

<img src="docs/psql.PNG" />