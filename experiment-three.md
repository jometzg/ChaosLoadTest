# Chaos Experiment Three

In this experiment we going to cause an issue with the node pool that the AKS cluster uses. We can then use our Azure Load Testing service to then run load tests:

1. before the experiment starts - to get a baseline
2. during the middle of a load test - to see how the experiment impacts a busy service
3. for the full duration of a load test - to get a better feel of the overall loss in performance

## Set up the Chaos Experiment

This chaos experiment uses the *VMSS Shutdown* fault. This allows you to designate the VMSS and how many of the instances in the pool get shutdown. 

![alt text](Humongous.Healthcare/images/chaos-node-pool-experiment.png "Node pool experiment")

This experiment only works well if there is more than one node in the node pool - otherwise the application (when on a single AKS cluster with a single node pool) will not work at all. A much more interesting experiment is a partial failure.


## Set up the Load Test 

No need to setup the load test, but it is useful to use the feature in load test that allows you to comment a run, so for a specific load test the purpose of the run can be recorded for later.

## Perform test runs

You can check that the experiment is having an effect on the cluster by looking at the node pools part of the the AKS instance in the portal. It should show one of the node pools not being available:

![alt text](Humongous.Healthcare/images/chaos-node-pool-failure.png "Node pool not ready")


### Run one - before the chaos experiment starts


### Run two - during a load test

![alt text](Humongous.Healthcare/images/chaos-node-pool-fault-during-test.png "Node pool issue during test")



### Run three - for the full duration of a load test

![alt text](Humongous.Healthcare/images/chaos-node-pool-fault-before-test.png "Node pool issue before test")


## Observations and Conclusions

This first conclusion that can be drawn is that in a two-node cluster, killing one node will not change the availability of the application.

But there is much more than this. What happens really depends on the scheduler, the deployment YAML's limits and what other workloads are competing for space on the cluster. If no limits are set, apart from not being good practice, it means that Kubernetes could schedule all replicas of the pod on the same node pool instance. If that node pool instance is killed during the chaos test, then they will be rescheduled onto the other node pool instance. 

Under more realistic conditions, the pods will have been scheduled across the node pool instances. Failure of one node pool instance, then means that either the workload will run with fewer instances or - if there is space that instance on the killed node pool instance will be rescheduled. Depending on the influence of the data tier, this may or may not have a noticable impact on the throughput of the application.


[Conclusions and future experiments](conclusion-future.md).


