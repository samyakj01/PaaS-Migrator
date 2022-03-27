# PaaSMigrator

This a Dot net based application and containerized.

This repo have Jenkins file for automating the following process:

1. Docker image creation.
2. Docker image upload to Azure Container Cegistry.
3. Docker container provisioning.

You can configure pipeline in your Jenkins instance (Docker also installed) by creating a Declarative pipeline.

Also, we have azure-pipelines yaml file to build and push docker image from Azure repository to Azure Container Registry.




