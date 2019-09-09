---
date: "2019-09-09"
authors: ["jmickey"]
slug: "kubecon-2019"
title: "KubeCon & CloudNativeCon 2019"
description: "My first KubeCon experience, and the takeaways from the conference."
featured_image: "/images/featured/barcelona-hero-image.jpg"
images:
  - "/images/featured/barcelona-hero-image.jpg"
categories: ["Community"]
tags: [
    "KubeCon",
    "Conferences",
]
toc: true
---

A little while ago (May 19th - 23rd) was KubeCon & CloudNativeCon EU. Held in Barcelona this year the conference welcomed over 7000 attendees through its doors, making it one of the largest tech conferences in the world. 

Thanks to my amazing employer - Condé Nast - I was lucky enough to attend the conference for the first time. In this post I'm going to talk about some of my favourite talks and take aways.

## Condé Nast Keynote

![Katie Gamanji giving a keynote presentation at KubeCon in front of thousands of attendees](/images/2019/09/katie-kubecon-keynote.png?"Katie giving her keynote at KubeCon EU 2019")

I want to start by congratulating my co-worker [Katie Gamanji](https://twitter.com/k_gamanji) on delivering an awesome 15 minute day-2 keynote on the "Centralised, Globally Distributed Cloud Platform" our team is building at Condé Nast. Katie provides a bit of detail on the motivations of moving towards a single platform, the components that make up that platform, and some important aspects of the developer experience. The recording can be found here:

<div style="position:relative;padding-top:56.25%;margin-top:1em;">
    <iframe src="https://www.youtube.com/embed/D7pbISekc8g" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

## Learning & Takeaways

### Service Mesh

I wouldn't hesitate to say that [Service Mesh](https://buoyant.io/2017/04/25/whats-a-service-mesh-and-why-do-i-need-one/) was one of the most talked about topics of the conference. With the two big players, [Linkerd 2](https://github.com/linkerd/linkerd2) and [Istio](https://github.com/istio/istio), at the centre of many of the 320+ sessions at the conference.

From what I could gather in my conversations with many other attendees - service mesh is something a lot of companies are thinking about, but still not something being very widely adopted yet. It's still quite a young technology, and I think many teams are still waiting to see how it matures...

#### Service Mesh Interface

They might not have to wait very long though, as one of the key announcements out of KubeCon & CloudNativeCon this year was [**Service Mesh Interface** (SMI)](https://smi-spec.io/). SMI is a joint effort by some big names including Microsoft, Linkerd, Hashicrop, Red Hat, and VMware (among many others) to provide a standard interface specification (similar to OpenTracing and Open Policy Agent) for service mesh products running on Kubernetes. 

SMI aims to deliver a basic set of standard APIs that all service mesh products will implement, allowing teams to change service mesh products within their clusters without the fear of losing essential functionality (or having to make complex changes to the way they use the service mesh product). Linkerd has already annouced they are working on implementing SMI. I've yet to see an official announcement from Istio, however there is an open issue [here](https://github.com/istio/istio/issues/14288). The announcement video for Service Mesh Interface is below:

<div style="position:relative;padding-top:56.25%;margin-top:1em;">
    <iframe src="https://www.youtube.com/embed/gDLD8gyd7J8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

### Observability

#### OpenTelemetry

The first big announcement in the observability space comes in the form of new developments in the [OpenTracing](https://github.com/opentracing/specification) and [OpenCensus](https://github.com/census-instrumentation/opencensus-specs) projects, with the two projects to be merged and re-launched as [**OpenTelemetry**](https://github.com/open-telemetry/opentelemetry-specification). OpenTelemetry will bring the OpenTracing tracing API together with the OpenCensus metrics API to form a new standard that will encompass both. 

Work has already begun to create a new set of API client projects that will provide feature parity with the existing clients from both projects. The current timeline is set to sunset the existing projects mid-November 2019 to coincide with KubeCon & CloudNativeCon North America. **I'm looking forward to seeing the evolution of these projects as OpenTelemetry begins to take shape!**

#### Fluent Bit

The next big announcement was from the creators of [Fluentd](https://www.fluentd.org/), with a new product called [**Fluent Bit**](https://fluentbit.io/). Fluent Bit, like Fluentd, is a pluggable log processor and forwarder but with a focus on performance. It currently supports over 30 plugins (versus ~650 available for Fluentd). Unlike Fluentd, Fluent Bit is written in C making it much more performant then its sibling.

Already there is a lot of talk of how teams can take advantage of the performance and size of Fluent Bit, with one interesting **take away** from the conference being the ability to utilise Fluent Bit within a Kubernetes cluster to collect, process, and forward logs from individual applications within the cluster into a centralised instance of Fluentd, where additional (less performance orientated) processing takes place.

#### Prometheus

I noticed that [Prometheus](https://prometheus.io/), a Cloud Native Computing Foundation (CNCF) owned project that focuses on the collection and aggregation of time-series metrics, got a lot of air-time this year. While there were no significant announcements regarding the project, a number of talks were focused on how different companies use and operate their Prometheus installations. Additionally, the number of projects that support Prometheus exporters continues to grow!

Of note however, is the introduction of projects designed to make the Prometheus experience easier on both developers and operators. With one such project, [Thanos](https://thanos.io) [GitHub](https://github.com/thanos-io/thanos), looking particularly interesting. Thanos allows teams to create highly available Prometheus offerings within their clusters, providing aggregation of metrics from multiple instances of Prometheus which can then be queries in a global query view, along with cost-efficient long term storage capabilities (e.g. AWS S3). Thanos is still in pre-1.0 development, but is already being used in production by a number of companies! **Definitely recommend taking a look!**

### Cluster API

[Cluster API](https://github.com/kubernetes-sigs/cluster-api) is a fairly new (currently in v1alpha2) Kubernetes project that provides a declarative, Kubernetes-native API to support cluster provisioning, configuration, and management. It allows for the creation and configuration of Kubernetes clusters via an existing cluster, including those that you would spin up via [minikube](https://github.com/kubernetes/minikube) or [kind](https://github.com/kubernetes-sigs/kind).

Prior to KubeCon I had not heard of Cluster API, but after a quick keynote by Joe Beda introducing the project, **I'm very keen to see how this project developers**, and will be keeping a close eye on it as a replacement to existing cluster bootstrapping projects such as kubeadm or kops.

## Favourite Talks

Below I will be showcasing some of my favourite talks from the conference!

### 1. Autoscaling Multi-Cluster Observability with Thanos and Linkerd (Andrew Seigner & Frederic Branczyk)

This was a great talk that showcased the power of Thanos by demonstrating application Horizontal Pod Autoscaling (HPA) across 4 clusters running in 4 different cloud providers, utilising Thanos to provide cross-cluster metrics.

<div style="position:relative;padding-top:56.25%;margin-top:1em;">
    <iframe src="https://www.youtube.com/embed/qTxunwzYO0g" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

### 2. Ready? Deep Dive into Pod Readiness Gates for Service Health Management (Minhan Xia, Ping Zou)

This talk provides a fantastic overview of the pod readiness workflow in Kubernetes, and how Pod Readiness Gates (introduced in Kubernetes v1.14) improves reporting of application/service readiness.

<div style="position:relative;padding-top:56.25%;margin-top:1em;">
    <iframe src="https://www.youtube.com/embed/Vw9GmSeomFg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

### 3. Helm 3 (Bridget Kromhout & Jessica Deen)

Helm is a Kubernetes package manager currently in version 2. Bridget and Jessica provide a solid overview of the improvements being introduced in Helm 3, including the much awaited removal of Tiller, an in-cluster service currently required in order to use Helm.

<div style="position:relative;padding-top:56.25%;margin-top:1em;">
    <iframe src="https://www.youtube.com/embed/lYzrhzLAxUI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

## Conclusion

My first KubeCon & CloudNativeCon was a great experience! I met some awesome people while partaking in the **End User Summit**, a Day 0 event specific to End User companies, and the conference [hallway track](http://www.meetings-conventions.com/Resources/Planner-Basics/Promoting-the--Hallway-Track-/). I gained some valuable insight about how other companies/teams are managing the complexity of their Kubernetes clusters, and the problems they're facing (a common theme was **developer experience**). 

Despite the long walk between the sponsor hall and the session room, and the not-so-great lunch offering, I'm very glad I had the opportunity to attend, and highly recommend it to anyone who is on the fence about attending next year. Hopefully I will see you there!
