
# Operator Overview
**General purpose of an operator: extend the functionality of a k8s cluster** <br>
If you want to know deeply how operators work, you need to understand two basic core concepts in k8s: *Resources* and *Controllers*

## Resources and Controllers 

Every time you run this command
```shell
kubectl create example_resource c
```
It will only write datas to store, it doesn't actual make `example_resource` appear in the cluster, the controller will do this job. There are many controllers running,
each cluster is se to watch a specific portion of the store that contains data about what that controller is responsible for.
The process of changing/updating resouces on controllers often involve other k8s component or non-k8s component (system exterior). After the controller has changed the running
state to matchthe requested state, it returns to watch the store, waiting for something new to change. <br>
=> This watch-change-watch loop is the central process that all of Kubernetes is based on <br>
=> And, **Operators** are meant for adding new watch-loops to clusters.

## Operators
An operatos consist of two parts
* a custom resouce definition (CRD): it contains the data needed to represent whatever functionality the operator is providing.
(*A custom resource is the API extension mechanism in k8s. A custom resource definition (CRD) defines a CR and lists out all the configuration availabe to users of the operator.A CRD allows you to extend the Kubernetes API. A CRD needs a Controller to act upon its presence (i.e., CRD instance).Without a controller for your custom resource, then it’s just a stateless object within Kubernetes.*)
* a controller process: runs in one or more pods.

![crd_controller](https://user-images.githubusercontent.com/12546802/127771536-c8865e3f-7ae4-49a1-bea7-7b6464c29901.png)


It could be understood that an operator is a custom k8s controller that uses custom resources (CR) to manage applications and their components. High-level configuration and settings are provided by the user within a CR. The k8s operator translates the high-level directives into the low level actions, based on best practices embedded within the operator's logic. 



=> They function the same way as the core k8s controllers do. <br>
=> They set a watch loop that waits for user input, and then starts and stops things to reflect that input. <br>
=> You can control and modify the system the same way k8s runs itself.

## Conventional versus Operator based Deployments
![conventional_vs_operator](https://user-images.githubusercontent.com/12546802/127771660-94beb894-5141-4afc-9883-5c8a7bc831aa.png)

=> You only need to configure and deploy instances of your operator instead of deployments for various resources <br>
=> Less error-prone and helps buy consistency by offering you a way to templatize your conventional deployment as well as allow you to develop domain-specific operations (operational knowledge) into your Operator via a controller implementation

## When to use an operator
It is important to know that all operators are controllers but not all controllers are operators. For a controller to be considered an operator, it must have application domain knowledge in it to perform automated tasks on behalf of the user (SRE/Ops engineer).
* Use an operator whenever you need to encapsulate your stateful application business logic controlling everything with Kubernetes API. This allows automation around your application built into the k8s ecosystem.
* Use an operator whenever you need to build a tool that watches your applications for changes and perform certain SRE/Ops tasks when certain things happen.

## References
1. https://developer.ibm.com/series/dive-into-kubernetes-operators/
2. https://www.magalix.com/blog/creating-custom-kubernetes-operators
3. https://www.redhat.com/en/blog/operators-over-easy-introduction-kubernetes-operators
