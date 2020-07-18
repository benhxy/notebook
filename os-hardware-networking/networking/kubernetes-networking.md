# Kubernetes networking

## Container network interface (CNI) and plugin
* Runtime: for example, a container orchestrator.
* Bare metal: for example, VM in cloud.
* CNI is created to standardize the network setup between runtime and bare metal.
* Runtime can pass a CNI config to a plugin running on it, so the plugin can fulfill that config (e.g. create virtual network interface, request and allocate IP address, update routing table etc.).

## Flammel

## kube-proxy




## Kubenetes DNS

## Egress masquerading (NAT)

## Service


## Service LoadBalancer (L4)

## Service NodePort (L4)

## Ingress (L7)

## Network policy

