## OpenShift for Developers - Digital

- Chapters 1 and 2 introduce OpenShift, its components, and its concepts.
- Chapter 3 shows you how to run OpenShift on your computer so that you have a virtual cluster to conduct the book’s exercises.
- In Chapter 4, you’ll configure OpenShift to fetch the source code for a simple Hello World application, build it into a container image, and run it.
- Chapter 5 introduces OpenShift Pipelines, a framework for composing Continu‐ ous Integration and Continuous Deployment (CI/CD) routines, and shows you how to add Pipelines to your cluster.
- In Chapter 6, you’ll deploy a more realistic application with a tiered architecture and multiple components.
- In Chapter 7, you’ll augment the application’s backend to retain data between sessions.
- Chapter 8 shows you how to examine, manipulate, and scale the running application both manually and automatically, how to set up OpenShift to periodically check application health, and how to govern the rollout of new versions of your application.
- Chapter 9 is a high-level overview of OpenShift’s monitoring and alerting facilities.
- Chapter 10 dissects OpenShift automation features you used along the way to set you on the path toward eliminating toil by letting the platform do the repetitive work.

### A Kubernetes Application Platform
OpenShift gives your applications distributed computing power without forcing you to become a distributed computing expert. Translated into jargon, that means OpenShift is a platform as a service (PaaS).

OpenShift includes tools for building applications from source in composable pipelines. It adds a browser-based graphical interface, the OpenShift Web Console, for deploying and managing workloads. You can point and click to set up network connections, monitoring and alerts, and rules for automatically scaling workloads. An OpenShift cluster applies software updates to itself and its nodes without cluster downtime.

OpenShift is a product from Red Hat. You can run it on your laptop, on a cluster of physical or virtual machines, on all the major cloud providers, and as a managed service. Like most software from Red Hat, OpenShift is developed as an open source project, the OpenShift Kubernetes Distribution (OKD). 

OpenShift is in turn built atop two open source keystones: application containers and the Kubernetes container orchestrator.

#### Linux Containers
Containers are an atomic unit of execution. Each running instance of a container is stamped from an Open Container Initiative (OCI) image that packages an application executable with all the pieces it needs to run. These dependencies can include shared libraries, auxiliary programs, language runtimes, and anything else the application requires. Such a self-contained parcel is easier to distribute among a team, in a con‐ tinuous series of releases on a server, and to arbitrary nodes in a cluster.

Container images are stored in a repository often called a container registry. Linux kernel facilities isolate and mediate running containers. A running container has its own filesystem and a defined share of the resources of the node where it runs. This isolation allows an orchestrator to schedule containers on a node with sufficient resources without evaluating every other workload running there for potential con‐ flicts in filenames, network port numbers, or other resources.

#### Kubernetes
OpenShift is a distribution of Kubernetes. Kubernetes is an open source project started at Google and developed by a group of companies and individuals since its release in 2014. This community has adopted formal governance through the Cloud Native Computing Foundation (CNCF). Red Hat has been a leading contributor to Kubernetes since the project began, and OpenShift is developed in collaboration with the Kubernetes community.

Kubernetes in OpenShift is like the Linux kernel in a Linux distribution. A Linux distribution combines the kernel with the more familiar programs you use directly. It also makes some basic choices about how you log in, where your files are stored, and what software is essential, letting you do useful work with the system without build‐ ing it entirely from scratch.

Kubernetes defines a set of common resources and an API for manipulating them. Those resources describe the desired state and track the actual state of the cluster and the things running on it. Kubernetes tries to make the actual state of a resource match its desired state. It repeats this for the life of the cluster. This continuous cycle of watching and tending is called the reconcile loop.

Kubernetes alone isn’t enough to sustain software in production. There are many decisions to make and components to configure before you can do much with it. Imagine you have the source code for an application and the job of deploying it on a Kubernetes cluster. How will you compile the source code or pair it with its interpreter for packaging in a container image? Will your build process need other computing resources, such as a specialized build server? Once the image is constructed, where will it be stored so that your cluster can access it? A public container registry (and external dependency) like Docker Hub or Quay? Or will you need to run your own registry? Your program likely depends on other programs, like a database or application server. Where and how will those run? Can you run them on the cluster, or will you have to maintain another system? These are basic considerations. Addressing them yields a running pod and a new set of questions: How should your application connect with the outside world? How should the power to scale the application, or deploy new versions of it, be governed?

#### What OpenShift Adds
OpenShift builds atop its Kubernetes core to add features and the components that support them. Some of its original developers called Kubernetes "a platform for building platforms." OpenShift took them up on it. It provides the automation and resilience of modern infrastructure while letting you stay focused on your application code (Figure 1-1).

 ![Image1-1](/images/image1-1.png)

 #### Web Console
 The OpenShift Web Console is a graphical view of the cluster and your applications. As the name suggests, it runs in a web browser. The Web Console lets you do everything necessary to deploy and run your software projects with graphical controls and forms for configuration, rather than sifting through so many lines and indentations of underlying YAML. The console depicts connections between services with a topological view of application components, and shows project, application, and con‐ tainer resource consumption with graphical gauges and charts (Figure 1-2).

  ![Image1-2](/images/image1-2.png)

  #### Curated Software Catalogs: An OpenShift App Store
  The Web Console also aggregates software catalogs, from application templates to Kubernetes Operators. The OperatorHub inside the Web Console, for example, is like an app store for Kubernetes applications. You can use it to find and deploy databases, message queues, and other middleware—the kinds of components nearly all applica‐ tions rely on. Like apps on your mobile device, Operators keep their applications run‐ ning and updated with the latest features and fixes.

  #### CI/CD: Pipelines
  OpenShift brings the continuous integration and continuous development (CI/CD) system into the cluster. OpenShift’s pipelines let you compose a process to build, test, package, and release your application. In this tutorial, you’ll go from logging in to the OpenShift Web Console to having the platform automatically build and deploy your code when you commit changes to your source repository. Once you establish deployment settings and build triggers, OpenShift should fade into the background of daily application development.

  #### Networking and Service Mesh
  OpenShift can simplify or even automate much of the tedious work of connecting application components together and to the outside world of your users and customers.
  
  OpenShift Routes configure an included Layer 7 reverse proxy for external HTTP connections to internal, load-balancing cluster Services. A Service is a stable endpoint representing the running pods of an application, since those may come and go with scaling, failover, or upgrades. A route specifies the external DNS hostnames for which it relays traffic and the Service to which that traffic should be directed.
  
  OpenShift also has a bolt-on service mesh, Istio. A service mesh measures and con‐ trols how services connect with one another and the outside world.

  #### Integrated Prometheus Metrics, Monitoring, and Alerts
  OpenShift constructs its features for monitoring cluster resources atop the open- source Prometheus project. The Web Console presents graphs showing CPU, mem‐ ory, and network usage for the whole cluster, a project, a deployment, or all the way down to a running container. Figure 1-3 shows the CPU usage of a deployment.

  ![Image1-3](/images/image1-3.png)

  OpenShift can gather application-specific metrics from programs that produce the standard Prometheus data format. Prometheus exporter libraries available for many languages equip an application to deliver statistics about its internal state in an interoperable way.

  #### Summary
  You’ve seen how OpenShift layers developer tools and application management atop Kubernetes to make it easier to deliver your software and keep it running. The next chapter introduces key concepts for building and deploying applications on OpenShift.

  ### OpenShift Concepts
  OpenShift is a superset of Kubernetes. Kubernetes concepts, commands, and practi‐ ces work on OpenShift. You can do any of the usual kubectl operations in the Open‐ Shift API. The reverse is not true. OpenShift has features and entire workflows that are not part of Kubernetes. For example, BuildConfig and Build resources in the OpenShift API represent the configuration and iterative executions of a process to build an application. They are not in the Kubernetes API, because Kubernetes doesn’t define a mechanism for compiling software and assembling container images. OpenShift adds these two types of resources and the facilities that use them. Likewise, while Kubernetes has a namespace to organize resources, OpenShift augments the namespace to form the Project. A Project demarcates access boundaries for clusters occupied by multiple tenants and serves as a discrete unit for administrative policy.

  Kubernetes establishes the components of a container orchestrator and a way of addressing them. OpenShift builds on that foundation, adding tools and abstractions for the developers who build the apps that run on the cluster. Keeping those apps running is the reason the cluster exists.

  #### Projects Organize Applications and Teams
  The Kubernetes namespace defines a scope for resource names. A cluster may be divided into any number of namespaces. Within a namespace, the names of resources must be unique. Namespaces partition a cluster among multiple applications, multiple application layers, or multiple users. To enforce access control or any security among those namespaces requires additional pieces and policies. OpenShift’s Project extends the basic namespace with default access controls (Figure 2-1).

  ![Image2-1](/images/image2-1.png)

  OpenShift enforces access control to the cluster and its resources. Details are beyond the scope of this book, but essentially, in OpenShift pluggable authentication modules govern authentification for an authorization regime built atop Kubernetes role-based access control (RBAC).

  RBAC rules define a user and make the user a member of at least one group. Groups are used to represent teams or units within a company that might need different levels of access to different Projects. Your user and group determine what resources you can see and what you can do with them. Projects, then, can be used to divide the clus‐ ter among multiple teams or multiple applications, enforcing the rules that keep them from interfering in other Projects. You can assign roles and the rights they entail to individual users, and users inherit roles from their group memberships.

  #### Projects and Applications
  Is a Project the same thing as an “application”? Projects divide the cluster into func‐ tional units, but they leave the ontology up to a cluster’s admins. On some clusters, a Project is dedicated to an application. Sometimes a Project is instead granted to a team, who might then run several applications in it, using labels to brand each appli‐ cation’s resources. OpenShift provides convenience features to apply and employ these labels to sort multiple applications in a Project. For example, resource icons can be grouped together by application in an OpenShift Web Console Topology view, like the components of sample-app shown in Figure 2-2.

  ![Image2-2](/images/image2-2.png)

  #### Application Components in OpenShift
  OpenShift represents an application as several abstractions, including the BuildConfig or pipeline for building that source and packaging the result in a container image, the configuration of how the running program should be deployed and scaled, and how it connects to the cluster’s network and potentially onto the wider internet in Figure 2-3.

  ![Image2-3](/images/image2-3.png)

  #### Pods
  The basic unit of running code in any Kubernetes cluster is the pod. A pod groups one or more containers together and guarantees they all run on the same cluster node. A pod has a unique IP address within the cluster, shared by all the containers in it. Containers in a pod can also share persistent storage volumes and memory, and can communicate with one another over the localhost interface.

  Pods are the unit of horizontal scaling. When a deployment is scaled up, new pods are created, usually on other cluster nodes. In a deployment’s specification, these are called replicas. Each replicated pod has the same set of containers and configuration but its own local runtime state.

  #### Services
  Each pod in a set of replicas has a unique IP address that can be reached from within the cluster. But the pods could be scaled up or down or be replaced by new pods in a failure or a rolling application update. The cluster provides an indirection through which you can reach a dynamic set of replicas. This is the Service abstraction. A service has an IP address and DNS name in the cluster. Connections there are routed to one of the pods in the set, even as the pods in the set are scaled or replaced.

  #### OpenShift Routes
  A Kubernetes Service is a load-balanced endpoint representing a set of pods. Usually there is an application running in those pods providing a service of some kind. A Service has a DNS name resolving to an IP address within the cluster, so it is uncompli‐ cated for other application components to connect to it. But that name and IP address are meaningless outside of the cluster. The rest of the office, the outside world, and the whole internet don’t know anything about them. Something has to connect outside traffic to the cluster Service living in the cluster’s logical network.

  Kubernetes provides the Ingress resource to define the wiring of outside connections to the cluster’s logical network. Ingress is a flexible, configurable representation of a network aperture and the rules under which it may be traversed. An Ingress resource requires an Ingress controller to satisfy its rules. An Ingress controller is a program that knows how to control an external network. There are Ingress controllers for reverse proxies, hardware load balancers, routers, and API-driven cloud provider networks, for example.

  The OpenShift Route is a simplified way to expose the most common HTTP and HTTPS services to networks outside the cluster. Creating a route associated with a Service causes OpenShift to configure its included reverse proxy with a DNS name and an IP address reachable from an external network. Connections to the route’s external IP address are then forwarded to the cluster Service, and from there on to an application pod.

  #### Building Container Images
  Before a pod fields requests coming in through a route to a Service, you must build the application. An OpenShift BuildConfig describes how to combine source code with a “base image” to create a new application container image. The base image usu‐ ally contains the tools for building source code in some programming language or framework. For example, there are Builder Images for common languages such as Java, Python, Go, and PHP. A BuildConfig can respond to webhooks, triggering builds in automatic response to changes to their base image or source code.

  #### Deploying Applications
  An application is built to be deployed. OpenShift’s Deployment defines the template from which new pods are stamped and the rules for recycling those pods when their configuration or their container image changes. For example, a deployment can begin a rolling update of its pods to deploy a new container image when a new build is triggered by a source code commit, or when a security update to a distribution requires a new base image. A deployment usually represents a single service or application component.

  #### Interacting with OpenShift
  There is more than one tool for using OpenShift, and the tools are different in their capabilities and intended users. All of the tools, however, are the same in how they talk to a cluster: through the OpenShift API. The Kubernetes core presents, and OpenShift extends, a REST API. In fact, any network client can communicate with the API, given authorized access and the OpenShift API reference documentation. This book does not go into detail on the subject, but API access is useful for integrat‐ ing with external systems; for example, an existing container-building process.

  #### oc
  The oc command-line tool is an OpenShift API client. It’s one of the main ways of interacting with an OpenShift cluster. Based on the same client-go library as the standard Kubernetes API client, kubectl, oc speaks all the kubectl commands as well as the superset of commands specific to OpenShift. While kubectl can scale a replica set to more pods, it doesn’t know anything about the OpenShift Routes you’ll soon use to connect outside traffic to your applications, for example. oc understands both, including the other important developer-oriented features like on-cluster builds, image streams, and the Projects that organize them.

  #### OpenShift Web Console
  The other tool you’ll get cozy with in this tutorial is the OpenShift Web Console, a graphical environment for deploying, managing, and monitoring your applications on OpenShift. The Web Console lets you see how application parts relate and how they consume cluster resources with topographical representations, graphs, and visual connections.

  #### Summary
  Now that you understand the relationship between OpenShift’s developer features and its Kubernetes core, you’re ready to put them to work.

  ### OpenShift Lab
  Log in to the OpenShift console via the instructions shared in the workshop.

  #### OpenShift Web Console
  The Administrator perspective of the OpenShift Web Console will allow you to handle all administrative tasks within the OpenShift cluster, such as working with users, nodes, workloads, and networking (Figure 3-1).

  ![Image3-1](/images/image3-1.png)

  #### Developer Web Console
  While technically you could accomplish deployments and builds of your application from within the Administrator perspective of the OpenShift Web Console, we will be working primarily in the Developer perspective. Switch perspectives by clicking on the upper-left dropdown and choosing Developer (Figure 3-2).

  ![Image3-2](/images/image3-2.png)

  Here you will see the Developer console that you will primarily be interacting with throughout the book. This console allows you to handle developer-related tasks such as deploying, building, and monitoring your application (Figure 3-3).

  ![Image3-3](/images/image3-3.png)

  #### Log In on the Command Line
  Usually, you would use your local command line interface (works on Windows, Linux or Mac). Since you might not be able to install anything for this workshop, you will use a terminal that was deployed for you into the workshop environment.

  Select the icon on the top right, next to the question mark - as seen below.

  ![Image3-4](/images/image3-4.png)

  After a few seconds, you will have access to a terminal with the oc tool installed.

  Initialize a new terminal and project as seen below, feel free to choose any project name.

  ![Image3-5](/images/image3-5.png)

  Run a few test commands to explore the oc tool:

  ![Image3-6](/images/image3-6.png)

  ```bash
  There is also a VSCode connector for the oc tool
  ```

  ### Deploying an Application on OpenShift
  You’ve got a handle on OpenShift concepts and you have access to an OpenShift cluster. Now you’ll use OpenShift to create a project, build the project’s application from source, and run it.

  #### A Simple Sample Application
  We will honor tech tradition by beginning with a “Hello World” program. This chapter’s simple program runs an HTTP service that prints a response to each request. We’ve selected the Go programming language because it compiles quickly and to demonstrate more than one language environments. You’ll use the Java Quarkus framework to build a more complex application in later chapters. OpenShift techniques you’ll use throughout the book, like on-cluster builds and automatic deployment, are largely agnostic about the language and frameworks you choose for a project.

  First, get a copy of the source code for the Hello World application. You’ll use Git to manage the source and GitHub to make your copy available for your cluster to build. Point your browser [to this chapter’s GitHub repository](https://github.com/openshift-for-developers/hello) to this chapter’s GitHub repository. Fork a copy to your own GitHub account with the Fork button at the top right. In Git terms, a “fork” is an exact copy of a repository at a point in time. You can modify your fork to create your own version or to make, test, and submit changes back to the original repo. You’ll use Git in this chapter, but you don’t need deep Git expertise; the following extremely brief overview of Git words and ways should get you started.

  #### Building and Deploying the Application on OpenShift
  The first thing you need is an OpenShift Project to contain the application resources. Log in to your cluster web console. There, the default account is “developer” and the password is also “developer”.

  Make sure you’re using the Developer perspective by checking or changing the selection to Developer using the OpenShift perspective switcher dropdown in the upperleft corner. Click on Topology. Create a new project by clicking the Project: All Projects dropdown and then click Create Project (Figure 4-1).

  ![Image4-1](/images/image4-1.png)

  In the Create Project dialog, configure the new Project, as shown in Figure 4-2.

  ![Image4-2](/images/image4-2.png)

  ```bash
  # Create a new Project in the OpenShift CLI by executing the following code:
        oc new-project \
        --display-name='Hello OpenShift for Developers' \
        --description='hello world' \
        o4d-hello
  ```

  Since you haven’t deployed anything, the Topology view will try to help out with a grid of things you might want to deploy. Choose From Git.

  The console will present a Git build configuration dialog, similar to that seen in Figure 4-3. Enter the URL of your forked Hello World source in your GitHub account: for example, https://github.com/<your-name>/hello.git. When you do, OpenShift will check the contents of the repository and, for known languages, will automatically select the appropriate Builder Image containing the compiler and other tools to build it.

  ![Image4-3](/images/image4-3.png)

  Check that Go is selected in the grid of Builder Images offered in the dialog. Otherwise, accept the defaults and click Create.

  ```bash
  # You can also do this through the oc cmd
  oc new-app golang~https://github.com/<your-name>/hello.git
  ```

  When you click Create, OpenShift will start building your source code with the Go compiler tools of the selected Builder Image. You’ll be returned to the console’s Topology view, which shows the application and updates its display as it builds and deploys (Figure 4-4).

 ![Image4-4](/images/image4-4.png)

 The application’s Topology icon conveys key information. Mouse over the badges on the icon’s edge and you’ll see that you can click through to build status, directly to the Git repository URL with the app’s source code, or to the external URL of a route to the application (Figure 4-5).

![Image4-5](/images/image4-5.png)

The status of the deployment is conveyed by different colors and tool tips. Dark blue indicates a running application, light blue one that is not yet ready, and red an application that needs attention because errors have occurred.

Click the Route badge to open the application’s external URL in your web browser (Figure 4-6).

![Image4-6](/images/image4-6.png)

#### Adding and Deploying a New Feature
Starting with a few lines of source code, you’ve used OpenShift to fetch, build, and deploy a stateless web application of contrived simplicity. Now imagine you are assigned a ticket for a feature request: change the displayed text to “Hello World!”. You can make this change and then have OpenShift rebuild the application and deploy the result, replacing the previous version.

This basic loop prepares you for two key ideas in the more elaborate application you’ll build through the rest of the book. The source-to-image build system on OpenShift will form the core of the more complete deployment pipeline you’ll create in Chapter 6. 

In later chapters, you’ll see how to set and change deployment strategies to keep services available during redeployments, or to deploy a new application version to only a subset of replicas, for single-cluster A/B testing.

##### Changing hello source
To address the text-change ticket, you need to change a string in the application source. If you’re a Git veteran, you may have cloned the repo to your local machine, and you already know how to edit with your preferred tool, commit, and push back to your GitHub repo. If that process isn’t familiar to you, don’t worry; for now, the needed change is simple enough to do it quickly in the GitHub web editor, and we will show you how to clone, change, commit, and send your changes back to your publicly visible GitHub repository before you need to do more involved coding.

Open the Go source file for your Hello World application, hello-openshift-for- developers.go, in your browser. Your copy will be at https://github.com/<your-name>/hello/blob/main/hello-openshift-for-developers.go. 

Change line 12 to "Hello World" as seen below. Make sure to commit your changes.

![Image4-7](/images/image4-7.png)

##### A new OpenShift Deployment
An OpenShift BuildConfig represents a source code location and a process for build‐ ing it into a deployable container. You already have a BuildConfig, created for building the Hello World app and reused each time a new release is deployed. Open the Builds view from the left menu of the Web Console’s Developer perspective. Then click on the hello-git BuildConfig to open it (Figure 4-11).

![Image4-11](/images/image4-11.png)

Start a build with the “Start build” item from the Actions menu at top right (Figure 4-12).

![Image4-12](/images/image4-12.png)

```bash
# It is possible to start the hello-git build using the command line by executing:

oc start-build hello-git
```

As shown in Figure 4-13, when the build completes, clicking on the URL icon in the Topology view will open the latest version of your application in a browser tab. Hello World!

![Image4-13](/images/image4-13.png)

### OpenShift Pipelines
OpenShift Pipelines is a CI/CD system based on the open source Tekton project. With Pipelines, you can trigger repeatable builds when source code changes, integrate tests into the process, and configure automatic redeployment strategies, from rolling updates to traffic-splitting A/B testing on a single cluster.

In this chapter, you’ll see how Pipelines integrates Tekton fundamentals with Open‐ Shift to make it easier to create and manage stepwise build and deployment processes.

#### Tekton
Tekton lets you create pipelines of repeatable steps. Tekton steps happen in a pod specifically created for the task. Tekton tasks are therefore isolated from one another and from the rest of the cluster, but you don’t have to manage a dedicated build server. Tekton’s moving parts are Kubernetes resources, so you can use familiar tools to create, manage, and monitor Tekton pipelines.

Tekton is the foundation of OpenShift Pipelines. Pipelines make it easier to set up, run, and monitor build processes by bundling the essential Tekton components and adding management tools in line with OpenShift conventions, including graphical representations of pipelines in the Web Console. You’ll see the two terms used interchangeably in this book, in Pipelines documentation, and in OpenShift CLI and GUI elements as well.

#### Using Pipelines
In the Web Console Developer perspective, you can create pipeline tasks and select reusable tasks to form pipelines, then run and observe them, check their log output, and control them graphically. On the command line, you drive pipelines with the OpenShift oc tool and a specific utility for pipelines called tkn. The tkn and oc command-line utilities are available in the OpenShift web user interface. 

Similar to the oc tool, we will be using the terminal in the OpenShift console.

```bash
# If you are a VS coder, be sure to check out the extension for Tekton Pipelines in addition to the OpenShift Connector for Visual Studio Code that we mentioned in Chapter 3. This extension allows you to graphically build a pipeline, and it connects to Tekton Hub for reusable pipelines and tasks shared by the community.
```

#### OpenShift Pipelines Resources
Tekton constructs pipelines from a list of Tasks, and therefore the Task is the basic unit of OpenShift Pipelines as well. 

A Task contains one or more steps. A Task occupies a pod, and each of its steps runs as a container in that pod. Tasks execute steps in serial order, starting each step on the completion of the one before it. A pipeline executes a set of these Tasks. 

Unlike the steps within them, all of a pipeline’s Tasks run at once in parallel unless a Task is configured to wait on another. A PipelineRun represents a single execution of a pipeline. Each run can be configured with parameters read from the environment or from programmatic input (Figure 5-5).

![Image5-1](/images/image5-1.png)

A Step is a series of commands that achieve a specific goal, such as building an image. Each Step runs sequentially in its own container inside a Task’s pod. Since the containers in a pod can optionally share resources, Steps in a Task can use common shared volumes, ConfigMaps, and Secrets.

#### Command
A command is a sequence of a named executable, any subcommand, and its argu‐ ments. In the following code for a command called generate, the command to run is the s2i Source-to-Image utility. This example command gives s2i’s build subcom‐ mand the --image-scripts-url argument with a filepath. It also references a parameter, the $PATH_CONTEXT, to set its value to the openjdk image:

```bash
- name: generate 
  command:
    - s2i
    - build
    - $(params.PATH_CONTEXT)
    - registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift
    - '--image-scripts-url'
    - 'image:///usr/local/s2i'
```

#### Script
A script puts an executable script inline so that a single Step that must run several operations can be more readably defined. An executable script can specify a command shell like bash or any language interpreter, such as python3 in the following example:

```bash
- name: lint-markdown 
  script:|-
       #!/usr/bin/env python3
       ...
```

Pipelines use other custom and native resources, like PersistentVolumes and claims, along with a set of parameters allowing for data persistence configuration of programs and scripts running in Steps or even between pod-isolated Tasks. Still, this look at the main elements should give you enough traction to apply pipelines in the next chapter to build an application with multiple components.

### Developing and Deploying from Source Code
Now that your local OpenShift has OpenShift Pipelines installed, you’re ready to deploy a multitier application. This app is more complex than your initial “Hello World” service from Chapter 4, as it has two components that need to communicate. The app also has been designed to eventually incorporate a database, as you will see in Chapter 7. You will hand some of these complexities off to a pipeline to automate some of the repetitive tasks of building and rebuilding the application through several iterations.

#### Noted: A Cloud-Ready Notes Application
Noted is a simple note board where each note contains a title and some content. When an optional database is connected, it will allow you to maintain the list of prior posts and delete them. It consists of two main components, a frontend and a backend, similar to how a typical web application might be architected.

The frontend is written in Node.js and uses the React library to display the list of posts. The posts call the quarkus-backend REST endpoint at /posts. While you will not be editing the frontend component of the app, you can find the source code for the [frontend app on GitHub](https://github.com/openshift-for-developers/nodejs-frontend).

The backend is written using Quarkus, a Kubernetes-native Java stack for microservi‐ ces and serverless development with fast startup times, hot reloads, a small memory footprint, and compact applications. The backend provides the /posts REST end‐point to the frontend app. Right now the lists of posts is volatile, stored only in memory. In Chapter 7, you’ll modify the quarkus-backend to use a database to main‐ tain the post list.

#### Application Topology
The easiest way to see the connectivity among components is through a topology view of the application (Figure 6-1).

![Image6-1](/images/image6-1.png)

Figure 6-2 shows the primary pipeline used to clone both the frontend and backend source code repositories, build the applications into images, and deploy them on your local OpenShift cluster.

![Image6-2](/images/image6-2.png)

> In Chapter 4, you deployed an application using the s2i build tool‐ ing in OpenShift. With OpenShift Pipelines, the build task will use buildah, and the deploy task will use the OpenShift CLI tool oc to handle deploying the image from OpenShift’s internal registry. However, your pipeline will be extensible, allowing integration of commonly used services like GitHub and Slack. It will also handle other tasks that Tekton can run. Check out Tekton Hub for some community-shared reusable tasks and pipelines.

#### Fork the Backend Repository
Before you deploy the application, you need to set up the GitHub repository for the quarkus-backend component. Open the book’s quarkus-backend repo and fork the repository by clicking the Fork button at the top-right corner, as in Chapter 4.

[Link to the backend](https://github.com/openshift-for-developers/quarkus-backend)

#### Create a New Project for the Noted App
Now that you have your Git repository, you can deploy the frontend and backend components to OpenShift:

1. Open the Developer console’s Topology view in your browser.
2. Create a new Project by clicking the dropdown next to the currently selected
project and then by clicking Create Project, as shown in Figure 6-3.

![Image6-3](/images/image6-3.png)

3. Configure the new Project as follows:
   1. Name: o4d-noted
   2. Display Name: OpenShift for Developers note
   3. Description: The Noted Application for the OpenShift for Developers

#### Deploy the Backend Component

Now deploy the quarkus-backend component to the new Project by clicking the +Add from the menu bar. Select the "Import from Git" tile. The main branch is what you will initially deploy, which is configured to operate without a database.

Next, configure the new application component. For the Git Repo URL, enter https://github.com/<your-name>/quarkus-backend.git. Click on “Show advanced Git options”; for “Git reference,” enter main; and for “Context dir,” enter /. Leave the Source Secret box empty. See Figure 6-4.

![Image6-4](/images/image6-4.png)

> A source secret is used if you are working with a private registry and you need to specify some secret such as an ssh key. See the CI/CD section of the OpenShift documentation for more details.

Continue configuring the quarkus-backend deployment. For Builder, make sure Java is selected. Under General, enter noted for the “Application name” and quarkus-backend for the Name (this is important for frontend/backend connectivity). Under Resources, make sure Deployment is selected. See Figure 6-5.

![Image6-5](/images/image6-5.png)

Continue to configure the quarkus-backend app by quickly adding a pipeline to build it from the source repository. Under Pipelines, check the “Add pipeline” checkbox. Under “Advanced options,” uncheck the Create a Route to the Application check‐ box, as this service does not need to be exposed externally. Then click Create (see Figure 6-6).

![Image6-6](/images/image6-6.png)

#### Inspect the Backend Resources
We can use the OpenShift CLI to inspect the backend resources. First you need to change the project you are working on to the newly created o4d-noted:

```bash
bash-4.4 ~ $ oc project o4d-noted
Now using project "o4d-noted" on server "https://172.30.0.1:443".
```

Now inspect the resources that were created. all is a useful shortcut for listing each standard OpenShift API resource that is common with deployment services, such as pod, service, route, deployment, replicaset, build, buildconfig, imagestream, job, and cronjobs:

![Image6](/images/image6.png)

When you are instantiating the quarkus-backend deployment, a few Kubernetes resources get created to manage the current state of the application. A replicaset is managed by the deployment resource and will keep track of and manage the desired versus available number of quarkus-backend pods that are running. A service also was created to spread the load across any other quarkus-backend components. You will see this in practice when you scale up the backend in the next chapter.

The output continues to show resources that are related to building the application as the pipeline resource configures native OpenShift resources to handle the build task. A buildconfig contains the configuration needed to instantiate a build for the container image from the GitHub repo. The imagestream provides the image registry location for the container image of the build.

Quite a few resources get created with the quarkus-backend deployment, but you may be wondering: where is the pipeline that created the buildconfig in the previous output?

```bash
bash-4.4 ~ $ oc get pipelines
NAME              AGE
quarkus-backend   12m
```

Notice that the all shortcut, as in oc get all, doesn’t match custom resources, so custom resource types don’t appear in a listing of “all”. Custom resources are nevertheless full-fledged resources. So you can describe them and do other common API operation “verbs” on them. You’ll learn more about generally working with API verbs, kinds, and objects, custom or otherwise, in Chapter 9. For now, describe the custom quarkus-backend pipeline custom resource to get an idea of how oc describe reveals object specification and status:

```bash
bash-4.4 ~ $ oc describe pipeline quarkus-backend
Name:         quarkus-backend
Namespace:    o4d-noted
Labels:       app.kubernetes.io/instance=quarkus-backend
              app.kubernetes.io/name=quarkus-backend
              pipeline.openshift.io/runtime=java
              pipeline.openshift.io/runtime-version=openjdk-17-ubi8
              pipeline.openshift.io/type=kubernetes
Annotations:  <none>
API Version:  tekton.dev/v1beta1
Kind:         Pipeline
Metadata:
  Creation Timestamp:  2022-04-21T23:18:27Z
[...]
```

The first section of the description includes the labels, annotations, and name. These labels are commonly used to organize and group components in your application:

```bash
Spec:
  Params:
    Default:  quarkus-backend
    Name:     APP_NAME
    Type:     string
    Default:  https://github.com/florianmoss/quarkus-backend.git
    Name:     GIT_REPO
```

The spec defines the parameters that are used in the pipeline. This configuration defines the default parameters, such as the Git repo and branch, for use in the instantiation of the pipeline, or pipelinerun:

```bash
 Tasks:
    Name:  fetch-repository
    Params:
      Name:   url
      Value:  $(params.GIT_REPO)
      Name:   revision
      Value:  $(params.GIT_REVISION)
      Name:   subdirectory
      Value:  
      Name:   deleteExisting
      Value:  true
    Task Ref:
      Kind:  ClusterTask
      Name:  git-clone
    Workspaces:
      Name:       output
      Workspace:  workspace
    Name:         build
    Params:
      Name:   IMAGE
      Value:  $(params.IMAGE_NAME)
      Name:   TLSVERIFY
      Value:  false
[...]
    Run After:
      fetch-repository
    Task Ref:
      Kind:  ClusterTask
      Name:  s2i-java
```

The Task stanza of the pipeline configuration lists all of the tasks that will be pro‐ cessed for this pipeline. Recall that Tasks execute in parallel unless they are configured to wait on each other, as shown by the Run After field in the preceding code.

#### Deploy the Frontend Component
Now you will deploy the frontend component of the Noted application.

In the Developer console, click +Add in the left column and choose the From Git tile. To configure the new nodejs-frontend component, enter https://github.com/openshift-for-developers/nodejs-frontend.git. Click “Show advanced Git options”; for “Git reference” enter main, and for “Context dir” enter /. Leave the Source Secret box empty.

Under Builder, make sure Node.js is selected. Under General, in the Application box enter noted, and in the Name box enter nodejs-frontend.

Under Resources, make sure Deployment is selected. Under Pipelines, check the “Add pipeline” checkbox. And under Advanced Options, check the “Create a route to the application” checkbox, and then click the link for the Deployment advanced option (see Figure 6-7).

![Image6-7](/images/image6-7.png)

> The Git repository URL configured is the nodejs-frontend reposi‐ tory under the book’s GitHub account. You are able to use this URL, instead of forking your own, as the following scenarios will not make any changes to the source code of the frontend.

Click the “Environment variables (runtime only)” link, and then enter the following for Name and Value, as shown in Figure 6-8:
    
    COMPONENT_QUARKUS_BACKEND_HOST quarkus-backend
    COMPONENT_QUARKUS_BACKEND_PORT 8080

![Image6-8](/images/image6-8.png)

In the Advanced Options of the nodejs-frontend deployment, you added two envi‐ ronment variables. These variables set the hostname and port of the quarkus-backend component within src/setupProxy.js so that the frontend knows how to retrieve the list of posts:

```bash
if (process.env.COMPONENT_QUARKUS_BACKEND_HOST) { backend_quarkus_host =
          process.env.COMPONENT_QUARKUS_BACKEND_HOST;
    }
if (process.env.COMPONENT_QUARKUS_BACKEND_PORT) { backend_quarkus_port =
          process.env.COMPONENT_QUARKUS_BACKEND_PORT;
    }
```

This hostname works, as the quarkus-backend deployment has a service that is named quarkus-backend. The service is accessible within the OpenShift cluster through the DNS hostname of quarkus-backend or the fully qualified domain name of quarkus-backend.o4d-noted.svc.cluster.local.

You can watch the progress of the build by clicking on Pipelines in the left sidebar, as shown in Figure 6-9. When both pipelines’ Last run status changes to Succeeded, the components are fully built and deployed, and you can test the application! To do so, open the Route to nodejs-frontend by clicking the Open URL icon in the Topology view for the nodejs-frontend. Note: The build process will take a few minutes. Better grab a coffee!

![Image6-9](/images/image6-9.png)

> List the pipeline runs in a project to inspect the current progress of the pipelines that are running using the OpenShift CLI by execut‐ ing oc get pipelineruns.

#### A Running Noted Application
Welcome to the Noted web frontend, and congratulations on deploying a cloud native application! Submit at least two posts with both Title and Content. You will notice the first bug in the application: each post’s title and content are displayed backward, as shown in Figure 6-10.

![Image6-10](/images/image6-10.png)

#### Automatic Pipeline Runs Using Tekton Triggers
Before you fix the display bug, it would be nice to set up some automation since you will be developing and rebuilding the quarkus-backend a few times. When you update your source code and push a commit to GitHub, a webhook or REST callback will trigger the pipeline to start and build the latest commit of your code. You need to set up a pipeline trigger to make this happen.

##### Pipeline Triggers
A pipeline trigger will create an EventListener pod in your project. This EventListener will also have an external URL, or route, that you can point the GitHub webhook to. This EventListener will run on OpenShift as a pod and will wait for GitHub to notify it about any source code change and act accordingly by running the corresponding pipeline.

To configure a trigger, in the Developer console, click Pipelines in the left column. Open the quarkus-backend pipeline. In the top right, click the Actions menu, and then click Add Trigger (Figure 6-11).

![Image6-11](/images/image6-11.png)

Now you’ll configure the new trigger. Under Webhook, enter github-push for “Git Provider type.” Under Parameters, enter quarkus-backend for APP_Name, https://github.com/<your-name>/quarkus-backend.git for GIT_REPO, and main for GIT_REVISION. Do not change the image_name, path_context, version, or work‐ space configuration. When you’re finished, click Add (see Figure 6-12).

![Image6-12](/images/image6-12.png)


#### GitHub Webhook Configuration
You need to configure GitHub to notify the trigger’s event listener.

1. Open your quarkus-backend repository on GitHub and click Settings, as shown in Figure 6-14.

![Image6-14](/images/image6-14.png)

2. Select Webhooks from the left sidebar and click the “Add webhook” button, as shown in Figure 6-15.
   
![Image6-15](/images/image6-15.png)

3. Now you’ll configure the webhook. For Payload URL, enter your trigger (see below where to find it), and for “Content type,” enter application/json. Leave the Secret box blank, as you do not need this field when using an event listener.

![Image62](/images/image62.png)

4. Check the Active checkbox and then click “Add webhook.”

#### The Reversed Text Quarkus-Backend Bug Fix
Now that your automation is configured, you can fix the title and content bug from earlier. The /posts endpoint is in the quarkus-backend Post.java source file.

1. First, open your quarkus-backend repository on GitHub and head to src/main/ java/com/openshift/fordevelopers/Post.java.

    Notice that lines 26 through 32 reverse the title and content strings:

```java
public String getTitle() {
    return new StringBuilder(title)
    .reverse().toString(); 
    // Should be: return title;
}
public String getContent() {
    return new StringBuilder(content)
    .reverse().toString();
    // Should be: return content;
}
```

Since the issue affects only two lines of the source code, it should be quick to edit using the in-browser editor on GitHub.

2. Click the pencil icon in the upper right corner to edit the source code. Update the code to fix the bug, as shown in Figure 6-17.

![Image6-17](/images/image6-17.png)

3. Commit the fix. Now it’s time to check out the pipeline and make sure the automation works as expected.

4. Open the OpenShift Developer console and click on Pipelines in the left sidebar. Notice that the quarkus-backend pipeline started automatically!

5. Click “quarkus-backend.” Click the Pipeline Runs tab, where you can see the status of all the pipeline runs for the quarkus-backend pipeline, as shown in Figure 6-19.

![Image6-19](/images/image6-19.png)

You can watch the output logs of the tasks in the pipeline. 

Once the pipeline run completes, open the nodejs-frontend application route by heading to the Topology view and clicking on the Open URL icon.

Notice that the posts you added earlier have been deleted because they were stored in an in-memory array that was reset when the backend was re-created. Add that bug to the backlog to handle later.

Now, add a post or two. As shown in Figure 6-21, you should notice that the title and the content are displayed correctly!

![Image6-21](/images/image6-21.png)

You might have noticed that all data was lost when we re-created the backend. Pods/Containers are ephemeral and don't store any data. You are not to manage databased, that's why we will ignore data persistence for this tutorial.

### Production Deployment and Scaling
Now that you have deployed the Noted application, we can talk about some basic tasks that you might need to perform to make the platform work for your app. 

First you will need to scale the quarkus-backend component to run multiple instances and handle more load. Since a few instances of your backend component will be running, we will discuss how OpenShift can deploy updates to the fleet and potentially roll out an update to your app with zero downtime using the proper deployment strategy for your specific application. OpenShift also has robust health checking built in to make sure things are running as expected, which we’ll cover in this chapter as well.

#### Application Scaling
OpenShift has some powerful built-in mechanisms in place that allow your application to scale by replicating. When a deployment scales upward its replica set creates additional pods for an application. The service associated with this deployment will perform the simple task of spreading the load across the replica set. The number of replicas that a deployment has can be configured manually or automatically based on CPU, memory, or concurrency metrics, as you will see and configure in the sections that follow.

##### Manual Scaling
Manually scaling the quarkus-backend deployment is a quick and easy way for your application to be able to handle more load.

Open the Topology view to manually scale the quarkus-backend. Select “quarkus- backend,” and click the Details tab in the slideout. Then click the ^ icon to deploy at least two quarkus-backend pods, as shown in Figure 8-1.

![Image8-1](/images/image8-1.png)

Increasing the count adds more pods to the deployment. OpenShift will attempt to run the desired number of pods as hardware resources allow. These pods use a service to load-balance the incoming quarkus-backend API requests.

```bash
#You can configure your application’s scale using the OpenShift CLI by executing 
oc scale --replicas=<desired replica count> <name>
```

#### The Service Abstraction
Services, introduced in Chapter 2, are a key component of how OpenShift makes scaling as simple as clicking an up arrow.

Click on the Resources tab in the quarkus-backend slideout and open the quarkus-backend service, as shown in Figure 8-2.

In Figure 8-2, you can see the details for the quarkus-backend service. This cluster-wide service has ports that are configured to be available via the cluster IP, or they can be more easily found at service-name.project-name.svc.cluster.local or in the case of quarkus-backend, quarkus-backend.o4d-noted.svc.cluster.local.

![Image8-2](/images/image8-2.png)

You can see all the pods that are load-balanced across this service by opening the Pods tab (see Figure 8-3). You may be wondering: how does the quarkus-backend service select the pods to be load-balanced?

![Image8-3](/images/image8-3.png)

#### Automatic Scaling
Scaling an application by clicking an up or down arrow is awesome and makes it so that you can quickly define how many replicas are available to your application. This allows you to manually grow your application to be able to handle more users. However, in most cases automated scaling is preferred in production environments as it will allow you to maximize the available resources to your application by reacting to its usage.

##### The Horizontal Pod Autoscaler
The Horizontal Pod Autoscaler (HPA) is one of the automatic scaling mechanisms built into OpenShift that will automatically scale your application deployment based on a CPU and memory threshold that you define. These metrics are captured using Prometheus, an open source monitoring solution that is included with the OpenShift Container Platform. You will explore Prometheus and OpenShift monitoring in Chapter 9.

To configure an HPA, you need a deployment that specifies memory as well as CPU requests and limits so that the HPA knows what to base the load threshold on. Therefore, you will need to edit the quarkus-backend deployment to add these metrics, as they were not configured in the deployment step in Chapter 6.

##### Update the quarkus-backend requests and limits
Requests and limits can be added at creation of a deployment or updated after an application has been deployed, as in the case of quarkus-backend. These simple configuration specifications define the minimum and maximum CPU and memory that deployments are allowed to consume. It is always recommended to configure requests and limits for every deployment on OpenShift. An application could clobber 100% of the CPU of the entire cluster at the expense of every other running workload on that individual node without the guardrails that limits and requests provide.

You can edit the configuration to add the requests and limits:

1. Open the Topology view. Select the quarkus-backend deployment, and in the Actions menu in the upper-right corner, select “Edit resource limits,” as shown in Figure 8-5.

![Image8-5](/images/image8-5.png)

2. Configure the Resource limit. For CPU Request choose “100 millicores”; for CPU Limit choose “1 cores”; for Memory Request choose “250 Mi”; and for Memory Limit choose “500 Mi.” When you’re finished, click Save. (See Figure 8-7.).

![Image8-7](/images/image8-7.png)

Rest assured, now the quarkus-backend will not be able to overrun the available resources for your OpenShift cluster due to the configured limits.

##### Configure a Horizontal Pod Autoscaler
The quarkus-backend now has CPU and memory limits and requests, so you are able to configure the Horizontal Pod Autoscaler to autoscale based on the load:

1.  Open the Developer console’s Topology view. Click on the quarkus-backend deployment icon, and in the Actions menu, click Add HorizontalPodAutoscaler, as shown in Figure 8-8.

![Image8-8](/images/image8-8.png)

2.  To configure the HorizontalPodAutoscaler, for Name choose “hpa-quarkus-backend”; for Minimum Pods choose “1”; for Maximum Pods choose “5”; for CPU Utilization choose “80%”; and for Memory Utilization choose “80%.” When you’re finished, click Save. (See Figure 8-9.)

![Image8-9](/images/image8-9.png)

Now the quarkus-backend is configured to autoscale once 80% of its CPU or memory limit has been consumed.

##### Verify autoscaling
Open the Details tab for the quarkus-backend in the Topology view. You will see the Pod Count displayed as Autoscaled to ..., indicating that OpenShift is automatically scaling this service (see Figure 8-10).

![Image8-10](/images/image8-10.png)

The quarkus-backend is now configured to automatically scale based on the load. You even configured limits to not allow it to grow out of control and take over all of the cluster resources.

#### Health Checks
Now that you don’t need to focus on manually scaling your Noted application compo‐ nents, you can rest easy knowing that it will always be available. What happens if the quarkus-backend is up and running in a noncrashed state but is not processing things as expected?

At the moment: nothing at all.

OpenShift’s health-checking functionality can automatically poll your application using HTTP, TCP, or container commands to verify that it is healthy. The poll’s response will be compared to a preconfigured expected value. OpenShift can attempt to redeploy a deployment with a failed health check as well as notify administrators about the health issue.

The quarkus-backend has a basic implementation of the quarkus extension SmallRye Health that is configured with a few health-checking probe endpoints defined in the following sections.

#### Health-Checking Probes
Health-checking probes provide the polling functionality to guarantee that your application is up, healthy, and responding as expected. There are three common health checks that you can configure when deploying your application on OpenShift: Readiness, Liveness, and Startup.

##### Readiness probe
A readiness probe determines whether a container is ready to accept service requests. If the readiness probe fails for a container, it will be removed from the list of available service endpoints. After a failure, the probe continues to poll the pod. If it becomes available, OpenShift will add the pod to the list of available service endpoints.

##### Liveness probe
A liveness probe determines whether a container is still running. The container will be killed if the liveness probe fails due to a condition such as a deadlock. The pod then responds based on its restart policy.

##### Startup probe
A startup probe indicates whether the application within a container is started. All other probes are disabled until the startup succeeds. If the startup probe does not suc‐ ceed within a specified period, OpenShift will kill the container, usually restarting it immediately after.

#### Configure the Health Checks in OpenShift
Now you are able to configure the health checking within OpenShift. This will instruct the cluster to begin polling the health endpoints of the quarkus-backend to verify that it is healthy and ready to process posts:

1. First, open the OpenShift Developer console’s Topology view. Then click on the quarkus-backend deployment, and in the Actions menu, click Add Health Checks.
2. We will configure only the liveness and readiness probes for the quarkus-backend. To do so, configure the health checks as follows. Start by adding a readiness probe by choosing HTTP GET in the Type field. Under HTTP Headers, for the Path enter /health/ready and for the Port enter 8080.


    Next, you will choose a series of thresholds:

    Failure threshold: 3
        The failure threshold is how many times the probe will try starting or restart‐ ing before giving up.

    Success threshold: 1

        The success threshold is how many consecutive successes are required for the probe to be considered successful after having failed.

    Initial delay: 30 seconds

        The initial delay is how long to wait after the container starts before checking its health.
    
    Period: 10 seconds

        The period is how often to perform the probe

    Timeout: 1 second

        The timeout is how long to wait for the probe to finish. If the time is excee‐ ded, the probe will be considered a failure.

3. Make your threshold selections. For Failure choose “3”; for Success choose “1”; for “Initial delay” choose “30 seconds”; for Period choose “10 seconds”; and for Timeout choose “1 second.” See Figure 8-11. Save your entries by selecting the checkmark button.

![Image8-11](/images/image8-11.png)

4. To configure the liveness probe, choose HTTP GET in the Type field. Under HTTP Headers, for the Path enter /health/live and for the Port enter 8080.

5. For the Failure threshold choose “3”; for the Success threshold choose “1”; for “Initial delay” choose “30 seconds”; for Period choose “10 seconds”; and for Timeout choose “1 second.”

6. Click add to save the updated deployment.

OpenShift can now programmatically detect whether the deployment is ready and working based on the health checks built into the quarkus-backend component. This offloads certain failure states that the health-check probes monitor to attempt to be automatically redeployed, resulting in fewer manual tasks for teams running production systems.

### Production Deployment Strategies
A few different types of production deployment strategies are available within OpenShift that allow you to determine how OpenShift handles rolling out your application in the event of an update, creation, updated scale, or if a pod was killed for some other reason.

#### Available Deployment Strategies on OpenShift
This section details the available strategies, as well as how the strategy that is used is determined by the constraints of the specific application.

##### Rolling deployment strategy
A rolling deployment is the default and most common deployment strategy within OpenShift. This method slowly replaces instances of the previous version of an application with instances of the new version of the application. If your deployment has heath checking configured, a rolling deployment will wait for new pods to become ready via a readiness check before scaling down the old components.

Rolling deployments are used when you would like updates with no downtime. One requirement of rolling deployments is that your application needs to support having old code and new code running at the same time. Typically, this requirement is not an issue in general deployments.

##### Canary deployments
A canary deployment is a common deployment paradigm that tests a new version of an application before rolling it out to the entire install base of that app. In fact, in OpenShift, all rolling deployments are canary deployments. The canary version, or the new version in a deployment update, is tested before all the old instances of that deployment are replaced. If the canary crashes immediately or if a configured readiness check never succeeds, the canary will be removed and the deployment will be automatically rolled back to the previously known working deployment.

##### Recreate deployment strategy
The recreate strategy has basic rollout behavior and could be used when your application is not able to run alongside an older version. This method will completely scale the deployment down to zero and then scale the deployment back up using the new version of your application. Be aware that using the recreate deployment strategy will incur downtime during updates as the deployment will scale down to zero for a brief period.

Recreate deployment strategies can also be used during one-time migrations or other data transformations before your new version starts; just switch the strategy for the update. Recreate deployments also need to be used when you want your deployment to use a persistent volume with strict writing requirements that specify that only one pod can mount the volume at a time. To put it another way, recreate deployments need to be used when the deployment needs to be configured to mount the volume with the access mode of read-write-once.

##### Custom deployment strategy
Custom deployments are...custom! You can customize how your deployment rolls out on OpenShift if the application has specific needs. This type of deployment strategy allows you to run custom commands for each rollout, and you are able to base your deployment rollout on the specific needs of a given application as well.

I can't see you using this one, but it's worth knowing that it exists.

#### Configuring a Deployment Strategy
You can easily configure rolling or recreate deployment strategies using the Devel‐ oper console.
Open the Developer console Topology view.

Select “quarkus-backend,” and in the Actions menu, click Edit Update Strategy. Notice how to change the strategy, and then click Cancel, as shown in Figure 8-13.

![Image8-13](/images/image8-13.png)

#### Deployment Rollbacks
OpenShift makes it easy to roll back a deployment if something doesn’t work cor‐ rectly with your rolled-out version. You can use the OpenShift command line to determine the rollout history for a specific deployment and then perform the roll‐ back, as shown here (the latest revision will be at the end of the rollout history list):

```bash
bash-4.4 ~ $ oc rollout history deployment/quarkus-backend
deployment.apps/quarkus-backend 
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
3         <none>
4         <none>
5         <none>

bash-4.4 ~ $ oc rollout undo deployment/quarkus-backend --to-revision=<Revision Number>
    deployment.apps/quarkus-backend rolled back
```

While your revision numbers may differ, you can validate that the quarkus-backend has been rolled back by listing the history again: