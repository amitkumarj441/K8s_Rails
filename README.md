# K8s_Rails
Deploy Rails based application on Kubernetes

# Prerequisites

## Secrets

We'll start by creating a Kubernetes secret. This secret contains the secret key base and database credentials required by the Rails application. To generate a secret key base, run

```
$ bundle exec rake secret
8d428e9d27e3323f1b1ec0089482017480224c9984fc10327f95b0990ec46175d43d756fd644c3bca3703a337a94ced69c868ab0470ac201cd1b6a80c3f89e4a
```

Encode the secret key base using base64.

```
$ echo -n "8d428e9d27e3323f1b1ec0089482017480224c9984fc10327f95b0990ec46175d43d756fd644c3bca3703a337a94ced69c868ab0470ac201cd1b6a80c3f89e4a" | base64
OGQ0MjhlOWQyN2UzMzIzZjFiMWVjMDA4OTQ4MjAxNzQ4MDIyNGM5OTg0ZmMxMDMyN2Y5NWIwOTkwZWM0NjE3NWQ0M2Q3NTZmZDY0NGMzYmNhMzcwM2EzMzdhOTRjZWQ2OWM4NjhhYjA0NzBhYzIwMWNkMWI2YTgwYzNmODllNGE=
```

Next, encode the database credentials. Use the format DB_ADAPTER://USER:PASSWORD@HOSTNAME/DB_NAME. If you are using mysql with a user 'deploy' and a password 'secret' on 127.0.0.1 and have a database railsapp, run

```
$ echo -n "mysql://deploy:secret@127.0.0.1/railsapp"
bXlzcWw6Ly9kZXBsb3k6c2VjcmV0QDEyNy4wLjAuMS90b2Rv
```

# Run

```
$ kubectl create -f railsapp_secrets.yaml
$ kubectl create -f railsapp_deployment.yaml
$ kubectl create -f railsapp_service.yaml
```

Check status 
```
$ kubectl get secrets
$ kubectl get deployments,pods
$ kubectl get services
```

# Test your app

To get the Minikube IP, run `minikube ip`. On my local machine, the app is available on `192.168.99.100:31596`.
Or run `minikube service railsapp-svc` 
