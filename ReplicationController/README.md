## ReplicationController
- A ReplicationController ensures that a desired number of pod replicas are running at any one time.
- A ReplicationController makes sure that a pod or a homogeneous set of pods is always up and available

### Working style of ReplicationController
- ReplicationController creates if less number of pods are available or terminates extra pods if there are too many pods
- It replaces if any one of pod is deleted or failed. for this reason, use ReplicationController if if your application require only single-pod
- ReplicationController supervises multiple pods across multiple nodes
- ReplicationController is often abbreviated to **rc** or **rcs** in discussion, and as a shortcut in kubectl commands.

![ReplicationController](https://github.com/javahometech/kubernetes/blob/master/images/ReplicationController.png "ReplicationController")
