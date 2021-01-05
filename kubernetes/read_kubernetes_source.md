# How to read Kubernetes source code

## Overview
* This doc explains the structure of Kubernetes source code and highlights the important directories.
* To better view Kubernetes source code, clone the code to local directory, and use VS Code + Go extension + Go Outliner extension. Go Outliner extension shows all types, functions, variables and constants in a package. This is especially useful because Go code in a packaged can be scattered in many files and are not ordered by types.
* Another way to view source code is on go.dev. For example, [this view](https://pkg.go.dev/k8s.io/kubernetes/pkg?tab=subdirectories) is useful to see all package descriptions, if any.
* The best way to understand what a package does is to read the unit test files. This is also Go's idiomatic way of documentation and showing samples.
* Kubernetes source code more or less follows the [common project layout](https://github.com/golang-standards/project-layout). Read it to help you understand the directories.

## /cmd
* This is where all the executable binaries are built from. Each child directory contains a main package, contains the main() function.
* This is a good starting point if you want to dig into a specific component (e.g. kube-apiserver, kubelet, kubctl).
* Most likely the core logic of the binaries are under /staging/src/k8s.io or /pkg. (e.g. the logic of /cmd/kube-scheduler lives in /pkg/scheduler)

## /cluster
* Scripts and manifests to speedily set up a cluster on GCE.
* These content is also used by Google to spin up GKE clusters.

## /staging/src/k8s.io, /pkg, and /vendor
* This is where most important library packages are located.
* /pkg was the original location. The community started to gradually migrate packages to /staging/src/k8s.io. Eventually all packages will migrate to separate repos.
* Sub-directories of /staging/src/k8s.io are synced to other git repos labeled with "k8s-staging" (e.g. https://github.com/kubernetes/kubelet). Those repos are then built, published, and imported as dependencies back to github.com/kubernetes/kubernetes.
* Inside the repo, these codes are resolved and imported from /vendor/k8s.io by symlinks.

## /staging/src/k8s.io/apimachinery
* This directory is connected to github.com/kubernetes/apimachinery.
* This is a collection of libraries that provide meta-structures and utilities for Kubernetes API types.
* It is very low on the dependency tree.
* More information: https://www.youtube.com/watch?v=w0y7ffx-GtY
* Package version and va/v1beta1: kubernetes API/type system (group + version + kind).
* Package runtime: Does things like reflection for kubernete's type system.
* Package label and selcetion: kubernetes API's label system.

## /staging/src/k8s.io/api
* This directory is connected to github.com/kubernetes/api.
* This directory contains API definitions by API groups in Go language. Each child directory contains API definitions of a group. Each group has its own versioning. Most of API structs are in ```./<version>/types.go``` file in each group's root directory.
* ./core: The most essential API object types, such as Container, Pod, Volumn, ConfigMap. This group of API is also served in REST path /api/v1. More on [Paths for API and API groups](https://www.oreilly.com/library/view/managing-kubernetes/9781492033905/ch04.html). This group's string representation in GroupVersion is empty string ```""```.
* ./app: Higher-level API object types based on core group, such as Deployment, ReplicaSet.

## /staging/src/k8s.io/client-go
* This is a library used by almost everything in kubernetes to talk to kube-apiserver. 
* Package transport: It wraps around a go http RoundTripper, and provides utilities like caching, TLS config.
* Package rest: It wraps around a go http client, and provides data access (e.g. GET, PUT, DELETE) for kubernetes objects. 

## /staging/src/k8s.io/component-base
* This is a library used by almost every kubernetes binary for its utilities.
* Package cli/flag: Wraps around spf13/pflag and provides "kubernetes-flavored" flags/options.
* Package logs: wraps around klog and provides utilities such as sanitization.
* Package metrics: provides a way to collect and expose prometheus-style metrics.

## /staging/src/k8s.io/apiserver/pkg/server
* Package server contains the plumbing to create kubernetes-like API server.
* This is also the base of kube-apiserver.
* Package options: A set of flags and options common to API servers (e.g. TLS config, etcd config).
* Package authentication/authorization: AuthN/Z for API access.

## Reference
* [Code base tour](https://www.youtube.com/watch?v=yqB_le-N6EE)
* [Building and running from source](https://www.youtube.com/watch?v=Q91iZywBzew)
* [Source code clusterfuck](https://www.youtube.com/watch?v=4VNDjwzzKPo)
* [TGI kubernetes](https://www.youtube.com/playlist?list=PL7bmigfV0EqQzxcNpmcdTJ9eFRPBe-iZa): Very good walkthrough per component/feature.