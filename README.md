# Chaos Studio Experiments with Azure Load Test

Azure Chaos Studio https://learn.microsoft.com/en-us/azure/chaos-studio/chaos-studio-overview is a new Azure tool for inducing faults in a target to allow you to really test how well an application or service copes with issues, specific outages, high CPU, low memory etc. This has often been difficult to test in a consistent way, so often development teams do not do this form of testing. This can lead to services being deployed that do not survive outages. Chaos Studio allows you to run "experiments" against a service (it must be emphasised that this should only be a test service) and see how it reacts to these experiments.

Azure Load Testing https://learn.microsoft.com/en-us/azure/load-testing/overview-what-is-azure-load-testing is a Azure's managed load testing service. This allows you to drive load into a service to see how it responds to high levels of load. Load testing really should be performed on all applications and Azure Load Testing simplifies the process of provisioning load test infrastructure and managing a series of tests and their results.

It is therefore natural to combine the use of both of these tools to test how an application or service copes with a problem when running at scale.

This repository is a workshop that combines the use of Chaos Studio with Azure Load Testing against an AKS-hosted API to Cosmos DB. The repository contains the code for the API and details how to deploy this to Azure and to then run combined chaos experiments alongside load tests to see the impact of an issue under load.
