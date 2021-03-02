- [Cloud Native Security](#cloud-native-security)
- [General Security Principles](#general-security-principles)
  * [Container Security](#container-security)
  * [Pod Security](#pod-security)
    + [SecurityContext](#securitycontext)
      - [Run as non-root](#run-as-non-root)
      - [Read only root filesystem](#read-only-root-filesystem)
      - [No new Privilege Escalations](#no-new-privilege-escalations)
      - [Seccomp](#seccomp)
  * [Cluster Security](#cluster-security)
    + [Apiserver](#apiserver)
    + [Kubelet](#kubelet)
    + [Kubeproxy](#kubeproxy)
  * [ETCD Security](#etcd-security)
      - [State](#state)
      - [Roles and bindings](#roles-and-bindings)
      - [Secrets](#secrets)
      - [Certificates](#certificates)
    + [AdmissionControllers](#admissioncontrollers)
      - [Node Restrictions](#node-restrictions)
      - [Open Policy Agent](#open-policy-agent)
  * [Host OS Security](#host-os-security)
    + [Malicious process identification](#malicious-process-identification)
    + [IAM / SSH Access](#iam---ssh-access)
  * [Runtime Security](#runtime-security)
  * [Network Security](#network-security)
  * [Threat Detection](#threat-detection)
  * [Build Hygiene](#build-hygiene)
  * [Image Hygiene](#image-hygiene)
    + [Audit Logging](#audit-logging)
- [Best practices & Compliancy](#best-practices---compliancy)
  * [CIS Benchmarks](#cis-benchmarks)




# Cloud Native Security 

This document details how to securely run workloads in cloud native enviroments, the scope is Kubernetes v1.20 and touches master components as well as node components. Only open-source technology is referenced.

### Defense in depth


# General Security Principles

## Container Security


## Pod Security

### SecurityContext
A SecurityContext object contains security settings that will apply to all containers belonging to a pod.

#### Run as non-root
Developers are used to running containers as root in docker, which makes their life easier, but also that of a possible attacker.
This is why pods should never have containers that run as root. 

Below is an example of a pod manifest with runAsUser configured:

```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    runAsUser: 1000
```

This will mitigate against:

| Mitre ATT&CK Technique | ID |
|------------------------|----|
| Privilege Escalation   | TA0004  |



#### Read only root filesystem
We want to prevent the container to be able to write to the root filesystem so the underlying filesystem can't be tinkered with by a possible attacker. For any files that an application or service needs to write, a (external) volume must be mounted. The root filesystem itself can be set as read-only from the pod's perspective. 

```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    readOnlyRootFilesystem: true
```


This will mitigate against:

| Mitre ATT&CK Technique | ID |
|------------------------|----|
| Privilege Escalation   | TA0004  |


#### No new Privilege Escalations
Privilege escalation (such as via set-user-ID or set-group-ID file mode) should not be allowed from the pod's perspective.

```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    allowPrivilegeEscalation: false
```


This will mitigate against:

| Mitre ATT&CK Technique | ID |
|------------------------|----|
| Privilege Escalation   | A0004  |

#### Seccomp

At the very minimum the default Seccomp policy should be applied to all containers.
Ideally a specific profile tailored to the service of application should be created.


```
apiVersion: v1
kind: Pod
metadata:
  name: seccomp-demo
  annotations: seccomp.security.alpha.kubernetes.io/pod: runtime/default
spec:
  securityContext:
    runAsUser: 1000
```


## Cluster Security
### Apiserver
### Kubelet
### Kubeproxy

## ETCD Security
#### State
#### Roles and bindings
#### Secrets
#### Certificates

### AdmissionControllers
#### Node Restrictions
#### Open Policy Agent

## Host OS Security


### Malicious process identification
### IAM / SSH Access

## Runtime Security

## Network Security

## Threat Detection

## Build Hygiene

## Image Hygiene



## Audit Logging

# Service Mesh

# Best practices & Compliancy

## CIS Benchmarks 
https://www.cisecurity.org/benchmark/kubernetes/
