---
layout: default
title: Operator
permalink: concepts/architecture/operator
type: concepts
redirect_from: architecture/operator
abstract: "Meshery Operator controls and manages the lifeycle of components deployed inside a kubernetes cluster"
language: en
display-title: "false"
list: include
---

# Meshery Operator <img style="width:1em; inline; margin-bottom:10px;" src="{{ site.baseurl }}/assets/img/architecture/B203EFA85E89491B.png"/>

Meshery Operator is the multi-service mesh operator (a Kubernetes custom controller) that manages MeshSync and it's messaging broker.

Meshery Operator is a Kubernetes controller manager, otherwise known as a Kubernetes Operator. Meshery Operator manages the lifecycle of every Meshery component that is deployed or running inside of a Kubernetes cluster.

## Deployments

It is recommended to deploy one Meshery Operator per cluster.

[![Meshery Operator and MeshSync]({{ site.baseurl }}/assets/img/architecture/meshery-operator-and-meshsync.svg
)]({{ site.baseurl }}/assets/img/architecture/meshery-operator-and-meshsync.svg)

### Initialization Sequence

[![Meshery Operator and MeshSync]({{ site.baseurl }}/assets/img/architecture/meshery-operator-deployment-sequence.svg
)]({{ site.baseurl }}/assets/img/architecture/meshery-operator-deployment-sequence.svg)

## Controllers managed by Meshery Operator

### Broker Controller

Meshery broker is one of the core components of the meshery architecture. This controller manages the lifecycle of broker that meshery uses for data streaming across the cluster and the outside world.

See [Meshery Broker]({{site.baseurl}}/architecture/broker) for more information.

### MeshSync Controller

MeshSync Controller manages the lifecycle of MeshSync that is deployed for resource synchronization for the cluster.

See [MeshSync]({{site.baseurl}}/architecture/meshsync) for more information.

## Operator FAQs

### When is Meshery Operator deployed and when is it deleted?  
As a Kubernetes custom controller, Meshery Operator is provisioned and deprovisioned when Meshery Server is connected to or disconnected from Kubernetes cluster. Meshery Server connections to Kubernetes clusters are controlled using Meshery Server clients: `mesheryctl` or Meshery UI.  This behavior described below is consistent whether your Meshery deployment is using Docker or Kubernetes as the platform to host the Meshery deployment.

**Meshery CLI**
`mesheryctl` initiates connection to Kubernetes cluster when `mesheryctl system start` is executed and disconnects when `mesheryctl system stop` is executed. This behavior is consistent whether your Meshery deployment is using Docker or Kubernetes as the platform to host the Meshery deployment.

**Meshery UI**
Meshery UI offers more granular control over the deployment of Meshery Operator in that you can remove Meshery Operator from a Kubernetes cluster without disconnecting Meshery Server from the Kubernetes cluster. You can control the deployment of Meshery Operator using the on/off switch found in the Meshery Operator section of  Settings.

### Does the Meshery Operator use an SDK or framework? 
Yes, Meshery Operator used the Operator SDK.