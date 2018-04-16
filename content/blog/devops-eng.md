---
date: 2018-02-13T16:00:00+06:00
lastmod: 2018-02-13T16:00:00+06:00
title: Becoming a DevOps Engineer - Part 1
authors: ["jmickey"]
slug: becoming-devops-eng-p1
toc: true
---

# Becoming a DevOps Engineer

## Introduction

Broadly, **DevOps** refers to the re-modelling of IT culture to improve software delivery outcomes (e.g. speed, reliability, and stability) by fostering collaboration and shared objectives throughout all stages of the SDLC. The practical consequence of this ideological shift is the cumulation of a set of principles, practices, and tools which form the necessary foundation for DevOps to be successful within an organisation.

The aim of this blog post isn't to provide yet another overview of what DevOps is and isn't; a quick search of Google will produce enough attempts at this to last the reader a lifetime (although [this](https://theagileadmin.com/what-is-devops/) is my personal favourite). Nor will I be making an argument [for](http://www.spikelab.org/blog/devops-job-title.html) or [against](https://devops.com/double-edged-devops-job-title/) DevOps as a team or job title/role. The undeniable reality is that this is the chosen job title for companies seeking operations individuals that possess the **practical** skills required for a DevOps adoption to be successful (i.e. don't hate the player, hate the game). It is these skills and my own personal pathway to becoming a DevOps Engineer that I will be focusing on in this post.

## What is a DevOps Engineer?

According to [research by Indeed.com](http://blog.indeed.com/2016/08/18/what-are-hardest-jobs-fill-in-tech/), DevOps engineers are in high demand, and with a [median salary of over $100kyear across Australia](https://www.payscale.com/research/AU/Job=Development_Operations_(DevOps)_Engineer/Salary) it's easy to see why many IT professionals are looking for pathways into these positions. However, the same Indeed.com survey reveals DevOps engineers as some of the most difficult to recruit. In part, this is due to the lack of clear definition of the DevOps engineer role, and what skills they should possess.

During his time as Head of Operations at Puppet Labs, Kelsey Hightower described DevOps engineers as the "special forces" of an organisation, going on to say:

> The DevOps engineer encapsulates depth of knowledge and years of hands on experience. You're battle tested. This person blends the skills of the business analyst with the technical chops to build the solution - plus they know the business well, and can look at how any issue affects the entire company.

Now, it would be far too self-indulgent of me to say that I accurately fit this description, but it does help provide context as to the level of seniority and technical skills a DevOps engineer is expected to possess. They require both breadth and depth of knowledge spanning multiple business domains, including systems administration, software development, quality assurance, and business analysis. Now, let's take a look at the core skillset:

### Communication and Collaboration

As DevOps culture is centred in extensive collaboration, this skill should come as no surprise. A DevOps practitioner should be able to effectively communicate and collaborate not just with the development teams they work with, but with all areas of the business relating to software delivery (e.g. Business Analysts, Products Owners/Managers, Project Managers). It is vital that DevOps engineers effectively translate business goals into practical requirements, measurements, and outcomes; and subsequently present the success or failure of these outcomes backed with empirical data.

### Systems Administration

DevOps engineers require strong cross-platform operational knowledge and experience, which serves as the foundation for many of the other skills required. It also helps form much of the framework of the DevOps mindset surrounding operational complexity, scalability, stability, monitoring, security, business continuity and disaster recovery. Historically these concerns rested mostly in the hands of operations teams, while developers focused on writing code that was considered production-ready provided it worked when they pressed F5. Armed with this perspective, it becomes easier to effectively foster a DevOps culture.

#### Cloud Administration

With the introduction of public and private cloud platforms (e.g. AWS, Azure, OpenStack/Shift, CloudFoundry), the way we build and manage software has changed dramatically. In addition to providing classic VM-style infrastructure, these platforms also give development and operations teams access to a host of platform services. These services remove server management overhead by taking common infrastructure services (e.g. databases, message queues, load balancing), and abstracting them via well-built APIs, while removing access to the underlying OS. Consequently, it is important for DevOps engineers to understand this shift in mindset, and gain practical skills in managing these platform services.

### Software Development and the SDLC

It's a popular misconception online and elsewhere that DevOps Engineers should be System Administrators that are able to script, with in-depth coding/programming skills left as an optional extra. However, as DevOps focuses heavily on building and delivering software, and as someone who spent the majority of their career on the operations side of the fence, I believe the opposite to be true. While automation and scripting are important components of the DevOps skillset, it is vital that those working within the SDLC have a solid understanding of the practical challenges in creating, building, testing, and releasing software. Additionally, the need to build and maintain in-house tooling has resulted in many operations teams taking on the extra role of a product team that delivers software internally.

#### Continuous Integration (CI), Continuous Delivery (CD), and Continuous Deployment (CD)

These practices form the cornerstone of the DevOps engineers' skillset, and it's crucial to understand [what each term means](https://www.atlassian.com/continuous-delivery/ci-vs-ci-vs-cd) and the tools/platforms built to achieve them. TeamCity, Jenkins, CircleCI, Octopus, and a host of other CI/CD systems generally top the list of requirements on job postings. However, it's not the tool itself that should be the focus here, but a solid understanding of the concepts that each of these solutions are attempting to encapsulate. Such concepts include:

- Distributed version control - Understanding local/remote repos, branching, pull requests, and merging should be a basic requirement.
- Build tooling - It's important to understand the toolchains used to compile application code, examples include Gradle, Maven, make, MSBuild.
- Testing - Beyond just knowing the different types of tests (unit, integration, functional), an understanding of what each type of test is attempting to achieve, and more practically, how to write good tests in each instance.
- Package management - Both in terms of application dependencies and deployment artefacts. Additionally, versioning and artefact hosting (Nexus, Artifactory). Examples include NuGet, NPM, Maven, Tarballs, and even containers.
- Deployment strategies - Getting the artefact to its destination environment (test, stage, prod), in a repeatable manner, while minimising downtime and maximising feedback. Examples include reckless, blue/green, canary.

While understanding these concepts doesn't necessarily mean you understand CI/CD/CD, they are core to achieving the goals and realising the benefits of each practice.

### Operations Automation

Automation in this context goes beyond simply writing bash or PowerShell scripts to complete arbitrary tasks. The goal here is to bring value to the business by solving complex problems in simplistic ways. Distributed software systems are becoming more complex, and consequently the operational complexity to deploy, run, and scale them increases in kind. Solving these complexity problems often requires learning new concepts and tools, and adopting new platforms that enable **reliable**, **repeatable**, and **testable** automation. The concepts to focus on here include Infrastructure as Code, Configuration Management, Immutable Infrastructure, and Behaviour-Driven Development.

### Monitoring and Metrics

Successful adoption of DevOps requires strong feedback loops. If time-to-market, reliability, stability, performance, and customer satisfaction are the measures of DevOps success, then feedback loops are the measuring tape. Feedback loops are formed by gathering, analysing, and presenting the metrics surrounding application delivery pipelines, performance, and stability. DevOps engineers should understand the tools available to gather these metrics, and how to analyse and present them in a way that is valuable to both delivery teams and key business stakeholders.
