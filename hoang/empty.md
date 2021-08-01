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
* a controller process: runs in one or more pods.

=> Together, they function the same way as the core k8s controllers do. <br>
=> They set a watch loop that waits for user input, and then starts and stops things to reflect that input


## References
1. https://developer.ibm.com/series/dive-into-kubernetes-operators/
