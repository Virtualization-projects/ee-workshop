# Developing applications with Docker Desktop Enterprise

Docker Enterprise 3.0 is the first Containers-as-a-Service platform to that extends from the developer's desktop to production. Docker Desktop Enterprise offers developers the ability to create container-based applications quickly and easily, even if they have little prior knowledge of Docker or Kubernetes. Developers on Windows 10 can create both Windows and Linux applications and developers on macOS can create Linux applications with Docker Desktop Enterprise. Application templates enable development managers, application architects, and security teams collaborate and create  templates, enabling developers to quickly get started coding with pre-approved guardrails that follow company standards, while still allowing flexibility to innovate. Docker Enterprise is the first platform to support both Docker Swarm and Kubernetes orchestration and this also extends to developer desktops with Docker Desktop Enterprise, including the ability to ensure matching API versions through the use of Version Packs.

In this lab we'll use Docker Desktop Enterprise to create container-based applications locally. If you're also running the Docker Enterprise workshop you will have the opportunity to push these applications to the Docker Enterprise cluster using both Swarm and Kubernetes. 

Suggested workshop order:
* Task 1 - Task XX in this workshop can be run as a standalone workshop using only Docker Desktop Enterprise. 
* If running in conjunction with the [Docker Enterprise workshop](README.md) you can switch over and run Task 1 in that workshop to setup your Docker Enterprise environment.
* After completing Task 1 in the Docker Enterprise workshop you can return to this lab and complete Task XX - XX to push and deploy applications to your cluster.

>**System Requirements**

> You will need to have Docker Desktop Enterprise installed on your laptop with internet access in order to complete this lab. An XX-day evaluation license is included with the download of Docker Desktop Enterprise.
> * Windows 10: Docker Desktop requires Hyper-V features in Windows 10 so you will need Windows 10 Pro or Enterprise to successfully install it.
>   * [Download Docker Desktop Enterprise for Windows 10](https://download.docker.com/XX)
> * macOS: Docker Desktop requires macOS XX or later
>   * [Download Docker Desktop Enterprise for macOS](https://download.docker.com/XX)
> * You will also need a code editor. Instructions here demonstrate the use of Visual Studio Code (vscode), but any code editor should work.
>   * No knowledge of the code syntax is assumed.
>   * Some steps demonstrate the use of Docker plugins in vscode; many code editors have Docker plugins available that should function similarly. The plugins are not required and the equivalent command will be given to complete the step.

> **Difficulty**: Intermediate (assumes basic familiarity with Docker) If you're looking for a basic introduction to Docker, check out [https://training.play-with-docker.com](https://training.play-with-docker.com)

> **Time**: Approximately XX minutes

> **Introduction**:
>	* [What is the Docker Enterprise Platform](#intro1)
>	* [Overview of Docker Desktop Enterprise](#intro2)
> * [Overview of Orchestration](#intro3)
>   * [Overview of Docker Swarm mode](#intro3.1)
>   * [Overview of Kubernetes](#intro3.2)

> **Tasks**:
> * Using Docker Desktop Enterprise
>   * [Task 1: Configure Docker Desktop Enterprise](#task1)
>     * [Task 1.1: Admin settings](#task1.1) 
>     * [Task 1.2: Enable Kubernetes](#task1.2)
>     * [Task 1.3: Use Buildkit](#task1.3)
>       * _daemon.json_
>   * [Task 2: Create an Application Template](#task2)
>     * [Task 2.1: Clone the Demo Repo](#task2.1)
>     * [Task 2.2: Customize the Template Settings](#task2.2)
>     * [Task 2.3: Add a Custom Template Repository](#task2.3)
>   * [Task 3: Develop an Application with Docker Desktop](#task3)
>     * [Task 3.1: Scaffold the Application Template](#task3.1)
>       - Show `template` CLI too
>     * [Task 3.2: Start the Application](#task3.2)
>     * [Task 3.3: Live Code Changes](#task3.3)
>     * [Task 3.4: Customize the Application](#task3.4)
>     * [Task 3.5: Deploy the Application on Kubernetes](#task3.5)
>   * [Task XX: Using Docker Assemble](#taskXX)

> * Deploying to Docker Enterprise Clusters
>   * These tasks should be completed after completing Task 1 in the [Docker Enterprise](README.md) workshop
>   * [Task 4: Connecting to Docker Enterprise UCP and DTR](#task4)
>     * [Task 4.1: Client Bundles](#task4.1)
>     * [Task 4.2: Docker Context](#task4.2)
>   * [Task 5: Push to DTR](#task5)
>     * [Task 5.1: Push Images to DTR](#task5.1)
>     * [Task 5.2: Bundle the Application](#task5.2)
>     * [Task 5.3: Push Docker App to DTR](#task5.3)
>   * [Task 6: Deploy App to UCP](#task6)
>     * [Task 6.1: Deploy to Swarm](#task6.1)
>     * [Task 6.2: Deploy to Kubernetes](#task6.2)


## Document conventions

- When you encounter a phrase in between `<` and `>`  you are meant to substitute in a different value.

	For instance if you see `<your email>` you would actually type something like `myemail@host.com`

## <a name="intro1"></a>Introduction
JIM TO UPDATE -- Docker Enterprise provides an integrated, tested and certified platform for apps running on enterprise Linux or Windows operating systems and Cloud providers. Docker Enterprise is tightly integrated to the the underlying infrastructure to provide a native, easy to install experience and an optimized Docker environment. Docker Certified Infrastructure, Containers and Plugins are exclusively available for Docker Enterprise with cooperative support from Docker and the Certified Technology Partner.

### <a name="intro2"></a>Overview of Docker Desktop Enterprise
JIM TO PROVIDE

### <a name="intro3"></a>Overview of Orchestration in Docker Desktop
#### <a name="intro3.1"></a>Overview of Docker Swarm mode
A swarm is usually a group of machines that are running Docker and joined into a cluster. After that has happened, you continue to run the Docker commands you’re used to, but now they are executed on a cluster by a swarm manager. The machines in a swarm can be physical or virtual. After joining a swarm, they are referred to as nodes.

With Docker Desktop you have a single Docker node. Because it is a single node Swarm mode is not enabled by default but you can still enable Swarm mode if you want to test commands and features that are only available in Swarm mode, such as XX, XX...

In a multi-node clustered environment, Swarm mode uses managers and workers to run your applications. Managers run the swarm cluster, making sure nodes can communicate with each other, allocating applications to different nodes, and handling a variety of other tasks in the cluster. Workers are there to provide capacity to your applications. If you are completing the [Docker Enterprise workshop](README.md) along with these exercises you will have a remote cluster with one manager and three workers and later tasks will have you push images and deploy applications from your Docker Desktop system to the remote cluster.

#### <a name="intro3.2"></a>Overview of Kubernetes

Kubernetes is part of Docker Enterprise 3.0 in both Docker Desktop and Docker Enterprise clusters. Kubernetes deployments tend to be more complex than Docker Swarm, and there are many additional component types in Kubernetes. The Universal Control Plane (UCP) in Docker Enterprise clusters simplifies much of the complexities of using Kubernetes, but for those who want to use all that Kubernetes makes available Docker Enterprise provides a [compliant - XX link to kube conformance page](https://linkXX) version of Kubernetes. We'll concentrate on Pods and Load Balancers in this workshop, but there's plenty more supported by UCP 2.XX.

## <a name="task1"></a>Task 1: Configure Docker Desktop Enterprise
Docker Desktop Enterprise comes pre-configured so there is usually very little that is required after install. We will explore some of the optional administration settings in this section.

### <a name="task 1.1"></a>Task 1.1: Admin Settings
* Show admin-settings.json (lockable settings)
  * Windows location: `??`
	* Mac location: `/Library/Application\ Support/Docker`
* Show dockerdesktop-admin tool
  * Windows location: `??`
  * Mac location: `/Applications/Docker.app/Contents/Resources/bin`
  * `sudo ./dockerdesktop-admin --help`
    * `sudo ./dockerdesktop-admin app uninstall` to remove DDE and VPs (do not run!)
* install a Version Pack with dockerdesktop-admin tool
  * `sudo ./dockerdesktop-admin version-pack install <path to ddvp>`
	* Note that Desktop needs to be stopped to add a VP


### <a name="task1.2"></a>Task 1.2: Enable Kubernetes

Enabling Kubernetes in Docker Desktop only requires a single click.
	![](./images/kube_enable.png)
NOTE: Offline mode is supported when enabling Kubernetes in Docker Desktop Enterprise.

* do not click the "make kube default for `stack deploy` commands - we will deal with this later

Congratulations! Docker Desktop is now ready for applications and can use either Swarm or Kubernetes. Next up we'll BLAH.

### <a name="task1.3"></a>Task 1.3: Use Buildkit

Buildkit is great because BLAH...JIM TO ADD

By default, Docker Desktop uses Build.XX. Buildkit is not required for any exercises in this workshop but we will go ahead and enable it so you can see it in action in case you want to explore advanced build actions on your own.

1. Open daemon.json

```json
{
  "debug" : true,
  "experimental" : false,
  "features": { "buildkit": true }
}
```

## <a name="task2"></a>Task 2: 

## Common Issues

* Confirm that you are setting the environmental variable DTR_HOST to the DTR hostname.

## Conclusion

In this lab we've looked how Docker Enterprise can help you manage both Linux and Windows workloads whether they be traditional apps you've modernized or newer cloud-native apps, leveraging Swarm or Kubernetes for orchestration.

You can find more information on Docker Enterprise at [http://www.docker.com](http://www.docker.com/enterprise-edition) as well as continue exploring using our hosted trial at [https://dockertrial.com](https://dockertrial.com)
