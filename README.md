## Week 7 CI/CD
# CI/CD with Azure DevOps

__Configure CI/CD pipelines to deploy the Node Weight Tracker application for 2 environments: Staging and Production.__

Project environment:
![week-6-envs](https://user-images.githubusercontent.com/90269123/138599669-1a2ac0cb-9e71-4100-a3a7-eb1d9d0c2afa.jpg)



__Before using this project the following files should be edited:__
>./inventories/production/hosts &emsp;&emsp;&emsp;__*# production nodes ip's*__

>./inventories/staging/hosts &emsp;&emsp;&emsp;__*# staging nodes ip's*__

In group_vars:

>all.yml


__Read documentation in source files.__
#
## Continuous Integration
The YAML `azure-ci.yml` responsible for the CI pipeline.

__steps:__

1. Install npm in the source directory.
2. Archive the files.
3. Copy the files to the artifacts directory.
4. Publish it to azure DevOps artifacts.

## Continuous Deployment and Continuous Delivery
For the CI/CD I've created a pipeline which using Ansible to deploy the artifacts to the environments.

>*The whole process of deployment to the Staging environment is completely automated while for the deployment to the Production environment a approval is required*

The CD pipline in Azure DevOps:


As you can see, once a new artifact added to Azure DevOps Artifacts it triggers the CD to the Staging enviroment.

Example of how to use ansible for the whole process:


>Note: Ive linked to each pipeline(stage and prod) a variable groups from the library and passing them in the command line as extra vars and using them to fill the .env file variables.
some of them contain sensitive information and are therefore not exposed to all.

## Prerequisites for the project
#
1. __To provision the infrastructure I've used my previous project:__
https://github.com/Ilankulikov/Week_6

2. __To install all dependencies on the nodes and to deploy and run the application for the first time I've used this project:__ 
https://github.com/Ilankulikov/Week_6_Ansible 



