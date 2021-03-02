


# General Security Principles

## Layers & Redundancy

## Least Privilege (pod perspective)

## Attack Surface

## Vulnerability Scanning


# Security Categories

## Container Security


## Pod Security

### SecurityContext
A SecurityContext object contains security settings that will apply to all containers belonging to a pod.

#### Least privilege

A lot of developers are used to running containers as root in docker, which makes their life easier, but also that of a possible attacker.
This is why every pod should never have containers that run as root. 

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


### Audit Logging



# Best practices & Compliancy

## CIS Benchmarks 
https://www.cisecurity.org/benchmark/kubernetes/
