---
date: "2019-09-27"
authors: ["jmickey"]
slug: "getting-started-with-openfaas"
title: "Getting Started with OpenFaaS and the OpenFaaS Community Cluster"
description: "OpenFaaS is a highly portable Serverless platform for Docker and Kubenretes with a focus on developer experience!"
featured_image: "/images/featured/openfaas-banner.png"
images:
  - "/images/featured/openfaas-banner.png"
categories: ["Programming"]
tags: [
    "Serverless",
    "OpenFaaS",
    "Kubernetes"
]
---

[OpenFaaS](https://openfaas.com) is a platform for "Serverless Functions Made Simple". The official definition explains OpenFaaS as such:

> OpenFaaS makes it easy for developers to deploy event-driven functions and microservices to Kubernetes without repetitive, boiler-plate coding. Package your code or an existing binary in a Docker image to get a highly scalable endpoint with auto-scaling and metrics.

OpenFaaS is completely Open Source, and is the brain-child of [Alex Ellis](https://alexellis.io) ([Twitter](https://twitter.com/alexellisuk)), who is the Director of OpenFaaS Ltd, and works on the project fulltime. You can support Alex via GitHub Sponsors [here](https://github.com/users/alexellis/sponsorship).

In this post I'm going to go through the basic steps for getting OpenFaaS setup for local development, writing your first function, and then go over the steps to deploy that function to the [OpenFaaS Community Cluster](https://docs.openfaas.com/openfaas-cloud/community-cluster/).

## Pre-requisites

You'll need the following in order to follow along with this tutorial:

1. Docker - Docker Desktop is [available here for Mac & Windows](https://www.docker.com/products/docker-desktop)
2. [Git](https://git-scm.com/downloads)
3. A terminal - Bash, Zsh etc. If you're running on Windows you can use the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10)!

## Install OpenFaaS and the `faas-cli`

To deploy and test your functions locally, you'll need to run an instance of the OpenFaaS gateway, along with a back-end provider, on your local machine. The simplest way to do this is via [Docker Swarm](https://docs.docker.com/engine/swarm/) and the provided stack deployment script.

Start by cloning the `https://github.com/openfaas/faas` repo:

```bash
git clone https://github.com/openfaas/faas.git
```

Then initialize Swarm mode on your Docker daemon:

```bash
docker swarm init
```

The next step is the installing the `faas-cli`. If you're on MacOS and already have homebrew install then installation is as simple as:

```bash
brew install faas-cli
```

For manual installation, you can use the following command:

```bash
curl -sSL https://cli.openfaas.com | sudo sh
```

{{% tip class="info" %}}**Note:** You can run the above script without `sudo`, but further steps will be required.{{% /tip %}}

## Deploy the FaaS Stack

You should now have a single node Docker cluster, which is all we need to get the FaaS stack up and running. To deploy the stack run:

```bash
cd faas
./deploy-stack.sh --no-auth
```

{{% tip class="info" %}}**Note:** The `--no-auth` argument will allow you to interact with the faas stack without worrying about authentication, **do not** do this in production. {{% /tip %}}

Once the deployment is complete open a browser and naviage to [http://localhost:8080](http://localhost:8080) to load the UI.

![The OpenFaaS Dashboard](/images/2019/09/openfaas-local-dashboard.png"The OpenFaaS Local Dashboard")

You can try various functions from the OpenFaaS 'store' from within the UI. For example:

1. Click the "Deploy New Function" button.
2. Search for "Dockerhub Stats" and click it.
3. Click "Deploy".

The function should appear on the menu on the left, click it, and wait for the status to change to "Ready". Then enter your GitHub username in the "Request Body" field and click `Invoke`. At the time of writing this my main GitHub user account only has a single image uploaded to Docker Hub:

![Docker Hub Stats Function Invokation from the OpenFaaS UI](/images/2019/09/hubstats-jmickey.png"Hubstats Function Invocation for Jmickey")

## Creating Your First Function

Create a new directory in a location of your choosing called `openfaas-functions`, and change into that directory from your terminal. This is the directory that your function code will live inside.

OpenFaaS provides a variety of templates to help you get started. These templates can be listed using the `faas-cli`:

```bash
faas-cli template store list
```

You should receive an output similar to the following:

```noop
NAME                     SOURCE             DESCRIPTION
csharp                   openfaas           Official C# template
dockerfile               openfaas           Official Dockerfile template
go                       openfaas           Official Golang template
java8                    openfaas           Official Java 8 template
node                     openfaas           Official NodeJS 8 template
php7                     openfaas           Official PHP 7 template
python                   openfaas           Official Python 2.7 template
python3                  openfaas           Official Python 3.6 template
ruby                     openfaas           Official Ruby 2.5 template
node10-express           openfaas-incubator Node.js 10 powered by express template
ruby-http                openfaas-incubator Ruby 2.4 HTTP template
python27-flask           openfaas-incubator Python 2.7 Flask template
python3-flask            openfaas-incubator Python 3.6 Flask template
python3-http             openfaas-incubator Python 3.6 with Flask and HTTP
node8-express            openfaas-incubator Node.js 8 powered by express template
golang-http              openfaas-incubator Golang HTTP template
golang-middleware        openfaas-incubator Golang Middleware template
python3-debian           openfaas-incubator Python 3.6 Debian template
powershell-template      openfaas-incubator Powershell Core Ubuntu:16.04 template
powershell-http-template openfaas-incubator Powershell Core HTTP Ubuntu:16.04 template
rust                     booyaa             Rust template
crystal                  tpei               Crystal template
csharp-httprequest       distantcam         C# HTTP template
vertx-native             pmlopes            Eclipse Vert.x native image template
swift                    affix              Swift 4.2 Template
lua53                    affix              Lua 5.3 Template
vala                     affix              Vala Template
vala-http                affix              Non-Forking Vala Template
quarkus-native           pmlopes            Quarkus.io native image template
perl-alpine              tmiklas            Perl language template based on Alpine image
node10-express-service   openfaas-incubator Node.js 10 express.js microservice template
```

Lets use the `golang-http` template. Pull the template:

```bash
faas-cli template store pull golang-http
```

You can now create a new function based on the template using the `faas-cli new FUNCTION_NAME --lang LANG_NAME` command:

```bash
faas-cli new helloworld-go-http --lang golang-http
```
You should now have the following files within the directory

```noop
helloworld-go-http/handler.go
helloworld-go-http.yml
.gitignore
```

Take a look at the `helloworld-go-http/handler.go` file, and edit it slightly to contain the following:

```go
package function

import (
    "fmt"
    "net/http"
)

// Handle a function invocation
func Handle(req handler.Request) (handler.Response, error) {
    var err error

    message := fmt.Sprintf("Hello %s", string(req.Body)) // Edit this line

    return handler.Response{
        Body:       []byte(message),
        StatusCode: http.StatusOK,
    }, err
}
```

Your function will also be specified in the `helloworld-go-http.yml` file:

```yaml
version: 1.0
provider:
    name: openfaas
    gateway: http://127.0.0.1:8080

functions:
    helloworld-go-http:
        lang: golang-http
        handler: ./helloworld-go-http
        image: helloworld-go-http:latest
```

There are a few key elements to take note of and understand here:

- `gateway`: Specified the remote gateway. For local development you will use the local gateway you deployed earlier via Docker Swarm. This can be overridden in CI via the `--gateway` flag, or the `OPENFAAS_URL` environment variable.
- `functions`: A map of your functions. Right now you'll only have one function specified here, but you can add more to this later.
- `lang`: The language as specified when you ran `faas-cli new --lang`.
- `handler`: The **folder** that contains your `handler.go` file. This can be changed if you want to give the handler a different name.

Time to deploy your function to the local Docker Swarm environment. You can choose to build and push your function in separate steps, but the easiest way to deploy your function is to use the following command:

```bash
faas-cli up -f helloworld-go-http.yml --skip-push
```

The `faas-cli` will now build your function (in a Docker container) and deploy it to our local cluster. The `--skip-push` flag will prevent the `faas-cli` pushing the built container to the Docker Hub, which it will normally do by default.

Once the deployment is completed navigate to the OpenFaaS UI in your browser ([http://localhost:8080](http://localhost:8080)) and you should now see the `helloworld-go-http` function available in the sidebar. Click it and enter your name into the `Request Body` and click `Invoke`. Hopefully you should receive a response that looks something like this:

![helloworld-go-http Function Invocation](/images/2019/09/helloworld-go-http-result.png"helloworld-go-http Function Invocation")

## Deploy to the OpenFaaS Community Cluster

