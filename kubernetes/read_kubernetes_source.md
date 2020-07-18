# Understanding Kubernetes source code

## Overview
* This is a doc to explain the structure of Kubernetes source code.
* To better view Kubernetes source code, clone the code to local directory, and use VS Code + Go extension + Go Outliner extension. Go Outliner extension shows all types, functions, variables and constants in a package. This is especially useful because Go code in a packaged can be scattered in many files and are not ordered by types.
* Another way to view source code is on go.dev. For example, [this view](https://pkg.go.dev/k8s.io/kubernetes/pkg?tab=subdirectories) is useful to see all package descriptions, if any.
* The best way to understand what a package does is to read the unit test files. This is also Go's idiomatic way of documentation and showing samples.
* Kubernetes source code also follows the [common project layout](https://github.com/golang-standards/project-layout). Read it to help you understand the directories.
* To set up development environment, check this out: https://github.com/kubernetes/community/tree/master/contributors/devel

## /cmd
* This is where all the component binaries are eventually built from. Each child directory contains a main package, which is the starting point of that binary.
* This is a good starting point if you want to dig into a specific component (e.g. kubelet).

## /api/openapi-spec
* This directory contains /swagger.json, which is the spec of all Kubernetes API.
* This spec is used to generate or define the most fundamental data structures (struct) in Go language source code.

## /staging/src/k8s.io
* This is where most source codes are located.
* Children directories are synced to other Git repos labeled with "k8s-staging" (e.g. https://github.com/kubernetes/kubelet). Those repos are then built and published as dependent packages.
* Inside the repo, these codes are resolved and imported from /vendor/k8s.io by symlinks.
* The content in each directory is described in README.md files.

### ./apimachinery
* This is a library that provide meta-structures and utilities for Kubernetes API types.
* For example, it defines how versioning works (./pkg/version), what labels are (./pkg/labels).
* It is very low on the dependency tree.

### ./api
* This directory contains API definitions by API groups in Go language. Each child directory contains API definitions of a group. Each group has its own versioning. Most of API structs are in ```./<version>/types.go``` file in each group's root directory.
* ./core: The most essential API object types, such as Container, Pod, Volumn, ConfigMap. This group of API is also served in REST path /api/v1. More on [Paths for API and API groups](https://www.oreilly.com/library/view/managing-kubernetes/9781492033905/ch04.html). This group's string representation in GroupVersion is empty string ```""```.
* ./app: Higher-level API object types based on core group, such as Deployment, ReplicaSet.

### ./client-go
* Kubernetes API client library written in Go. It can be used to build other clients.

### ./apiserver
* A library for building API aggregator server.
* ./pkg/server: 
