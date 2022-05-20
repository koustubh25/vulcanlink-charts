# Chainlink Helm Chart
Helm chart deploying a [http://chain.link/](Chainlink) oracle node.

## TL;DR

```console
$ helm repo add koustubh https://koustubh25.github.io/charts/
$ helm install my-release koustubh/chainlink
```

## Introduction

This Chart is a fork of https://github.com/vulcanlink/charts with the following additions:
1. Postgres is now a part of this chart. It makes it easier to get up and running with chainlink
2. An infura node url is added for Ropsten network, so you don't need to stand up your own ethereum node

## Prerequisite
1. You should have kubernetes running. This can be easily done on local by installing [minikube](https://minikube.sigs.k8s.io/docs/start/) and then `minikube start`

## Install

1. 
```shell
$ helm repo add koustubh https://koustubh25.github.io/charts/
$ helm install my-release koustubh/chainlink
```

This will set up 2 pods viz. `chainlink` and `postgres`
2. Make sure the output of 
```
kubectl get pods -n default
```
gives  you healthy pods. If the pods are not healthy, check again in some time as it can take time for the pods to come up.

3. Most config is done in [this](values.yaml) file. Feel free to change it.

4. Once the pods are up, you are ready to port-forward the service
```shell
$ kubectl port-forward svc/test-chainlink 6688:6688 -n default
```
5. Go to the browser and hit `http://localhost:6688`. Enter the credentials configured in the config section of  [values.yaml](values.yaml) (`API_LOGIN`)