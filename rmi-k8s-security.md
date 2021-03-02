


# General Security Principles

## Layers & Redundancy

## Least Privilege (pod perspective)

## Attack Surface

## Vulnerability Scanning


# Security Categories

## Pod Security

### SecurityContext
A SecurityContext object contains security settings that will apply to all containers belonging to a pod.

#### Run as non-root

A lot of developers are used to running containers as root in docker, which makes their life easier, but also that of a possible attacker.
This is why every pod should never have containers that run as root. 

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
