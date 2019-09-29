---
title: Talks
weight: -270
---

Occasionally I give talks at meetups or conferences. A full history of my talks in the form of slides can be found on [SpeakerDeck](https://mickey.dev/speakerdeck). Below is a list of the most recent talks I've given, along with any video recordings that might exist.

## Rapid API Development in Go
**Presented:** [DDD East Anglia](https://dddeastanglia.com) (September 2019)  
**[Slides](https://speakerdeck.com/jmickey/rapid-api-development-in-go)** | **[Code Samples](https://github.com/jmickey/go-code-samples)**

The Go programming language is a statically typed, compiled programming language designed at Google that was released in 2009. It grew quickly in popularity - holding a top 5 position in the most loved programming languages in the Stack Overflow developer survey for 5 consecutive years, and in 2018 was the fastest growing language on GitHub.

Much of Go's popularity can easily be attributed to it's clear and concise syntax, simple concurrency model, strong built-in tooling, and its ability to be easily compiled into a single statically linked binary. However, to me Go's greatest strength is its robust, "batteries included" standard library, which allows developers to rapidly build production ready applications with little to no external dependencies.

In this talk I will provide a brief overview of the Go programming language, and demonstrate how Go can be utilised to rapidly build production ready APIs with just the standard library - HTTP(S) server and all. Finally I will provide a brief demo of a simple API workflow, and talk about some small libraries and tools that can be used to improve the development process and general quality of life.

## Utilising OSS to Operate a Centralised, Globally Distributed Cloud Platform
**Presented:** [Cloud Native London Meetup](https://meetup.com/Cloud-Native-London) (September 2019)  
**[Slides](https://speakerdeck.com/jmickey/utilising-oss-to-operate-a-centralised-globally-distributed-cloud-platform)**

Condé Nast is a global publishing powerhouse - home to some of the largest names in fashion and luxury print and digital publications. In an effort to provide a cohesive vision for these brands across more than 30 markets, a truly global platform was required. Utilising AWS and Kubernetes at its core, the platform officially launched in September 2018 and serves over 200 million unique visitors/month.

Of course, operating Cloud Native Infrastructure is more than just spinning up a container orchestrator! Auxiliary services are required in order to operate it effectively and provide developers with a true platform experience. Open Source Software (OSS) forms the backbone for much of what we do. As such, this talk will be focusing on how Condé Nast utilises OSS to effectively operate multiple Kubernetes clusters across the world, paying special attention to observability, testing, application delivery, and developer experience.

### Recording

[![Placeholder image for my Cloud Native London talk on Utilising OSS to Operate a Global Cloud Platform](/images/2019/09/cloud-native-lon-oss-talk.png)](https://skillsmatter.com/skillscasts/14461-cloud-native-september)

## Finding a Needle in a Call Stack - Intro to Distributed Tracing
**Presented:** [DDD Perth](https://dddperth.com/) (August 2019), [Cloud Native London Conf](https://skillsmatter.com/conferences/11723-cloudnative-london-2019) (Sept 2019)  
**[Slides](https://speakerdeck.com/jmickey/finding-a-needle-in-a-call-stack-intro-to-distributed-tracing)**

In this session I explore the basics of distributed tracing. I then take a look at the OpenTelemetry (formally OpenTracing) standard - a vendor neutral framework for distributed tracing instrumentation. Finally, I take a hands-on look at distributed tracing in action using Jaeger, a popular open source distributed tracing tool which is part of the Cloud Native Computing Foundation. By the end of this session I hope viewers will not only have a good understanding of distributed tracing, but will be equipped with the knowledge and inspiration to introduce it within their own applications.

[Video Coming]

## Killing Bugs with KINDness - Kubernetes in CI with K8s in Docker (KIND)

**Presented:** [Docker London](https://docker.london) (July 2019)  
**[Slides](https://speakerdeck.com/jmickey/kubernetes-in-docker-killing-bugs-with-kindness)**

KIND - Kubernetes IN Docker - is a relatively new tool for running Kubernetes clusters within Docker. KIND enables engineers to spin up local development cluster in under a minute, utilising Docker containers as "nodes". KIND was originally born as a method of running conformance tests for the Kubernetes project itself, and has quickly gained in popularity within the community thanks to its fast startup time, ease of use, and growing feature set. In this talk I will briefly look at how KIND differs from other local cluster tools, discuss a range of possible use-cases for KIND - both for local development and within CI/CD pipelines, and finally demonstrate how you can get starting using KIND.

### Recording
[![YouTube Placeholder Image](/images/2019/08/kind-talk-placeholder.png)](https://www.youtube.com/watch?v=D5ULwbER7PA&start=4800)

## Lessons Learnt: Over 70 Interviews in Just 5 Weeks
**Presented:** [Fenders Perth](https://www.fenders.co/) (November 2018)  
**[Slides](https://speakerdeck.com/jmickey/lessons-learnt-over-70-interviews-in-just-5-weeks)** |
**[Blog Post](/posts/80-interviews-across-planet/)**

5 weeks, 39 unique companies, and over 70 remote interviews. In this talk Josh will be sharing some of the lessons he learnt, and mistakes he made while searching for a job in the UK. He will present some interesting data on the interviews, discuss what he did right and wrong, the pain points he suffered, what he enjoyed, and finally - offers some advice for hiring managers and job seekers alike.

### Recording

{{< youtube wCfxY9HVkoU >}}

## Introduction to Terraform

**Prensented:** [Python & Django Meetup Perth](https://www.meetup.com/Perth-Django-Users-Group/) (March 2018)  
**[Slides](https://speakerdeck.com/jmickey/introduction-to-terraform)**

Introduction to Terraform for managing cloud infrastructure.