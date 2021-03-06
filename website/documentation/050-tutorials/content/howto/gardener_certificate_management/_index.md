---
title: Gardener Certificate Management
description: "Configure Certificate Management For Shoot Clusters"
type: tutorial-page
level: Advanced
index: 10
category: Certificates
scope: operator
---

# Gardener Certificate Management

## Introduction
Gardener allows Shoot clusters to request and receive verified X.509 certificates for Ingresses out of the box. 
Therefore, Gardener needs to be set up with certain configuration parameters.

## Gardener Helm Installation
If you choose to deploy Gardener via Helm, the following sections help you to set up certificate management for Shoot clusters.
### Configuration
The configuration for certificate management is passed as a value `.controller.certificateManagement` to the Gardener 
chart. An example of how the configuration looks like can be found in 
[10-secret-certificate-management-config.yaml](https://github.com/gardener/gardener/blob/master/example/10-secret-certificate-management-config.yaml).

> Since the certificate request is forwarded to Let's Encrypt which asks Gardener to prove the ownership of the Shoot 
> cluster's domain by **DNS01 challenges**, it is fundamental to add the respective cloud DNS provider account(s) to 
> this configuration. Usually, these are the same accounts used for Gardener's **Default Domains**.

<style>
#body-inner blockquote {
    border: 0;
    padding: 10px;
    margin-top: 40px;
    margin-bottom: 40px;
    border-radius: 4px;
    background-color: rgba(0,0,0,0.05);
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    position:relative;
    padding-left:60px;
}
#body-inner blockquote:before {
    content: "!";
    font-weight: bold;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    background-color: #00a273;
    color: white;
    vertical-align: middle;
    margin: auto;
    width: 36px;
    font-size: 30px;
    text-align: center;
}
</style>

### Feature Gate
To enable the feature itself, the Feature Gate `CertificateManagement: true` must be passed as a value `.controller.featureGates` to the Gardener chart.

```yaml
featureGates:
  CertificateManagement: true
```

## Local Development
If you want to enable certificate management for Shoot clusters in your Gardener development environment, please refer 
to the sections below.

### Configuration
The configuration for certificate management must be present as a **Secret** in the Garden cluster. An example of how 
the configuration looks like can be found in [10-secret-certificate-management-config.yaml](https://github.com/gardener/gardener/blob/master/example/10-secret-certificate-management-config.yaml).


> Since the certificate request is forwarded to Let's Encrypt which asks Gardener to prove the ownership of the Shoot 
cluster's domain by **DNS01 challenges**, it is fundamental to add the respective cloud DNS provider account(s) to this 
configuration. Usually, these are the same accounts used for Gardener's **Default Domains**.

### Feature Gate
To enable the feature itself, the Feature Gate `CertificateManagement: true` must be enabled in 
 [20-componentconfig-gardener-controller-manager.yaml](https://github.com/gardener/gardener/blob/master/example/20-componentconfig-gardener-controller-manager.yaml)


```yaml
featureGates:
  CertificateManagement: true
```