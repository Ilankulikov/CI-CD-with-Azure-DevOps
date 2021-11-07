## Week 7 CI/CD
# CI/CD with Azure DevOps

__Configure CI/CD pipelines to deploy the Node Weight Tracker application for 2 environments: Staging and Production.__

__In this project I have used everything we've learned so far and previous projects.__

## Prerequisites for the project

- __IaC with Terraform- Provisioning of two identical environments : [Week 6 project](https://github.com/Ilankulikov/Week_6) .__

- __Configuration Management with Ansible - Installing all the dependencies and deploying the application for the first time on the remote machines: [Week 6 Ansible project](https://github.com/Ilankulikov/Week_6_Ansible) .__ 

- __Node Weight Tracker - The Bootcamp application which you can find [here](https://github.com/Ilankulikov/bootcamp-app) .__

Project environment:
![week-6-envs](https://user-images.githubusercontent.com/90269123/138599669-1a2ac0cb-9e71-4100-a3a7-eb1d9d0c2afa.jpg)




__Before using this project the following files should be edited:__

**inventories**
- **production**
  - hosts &emsp;&emsp;&emsp;__*# production nodes ip's*__

- **staging**

  - hosts &emsp;&emsp;&emsp;__*# staging nodes ip's*__

**group_vars:**

- all.yml


__Read documentation in source files.__
#
## Continuous Integration
The YAML `azure-ci.yml` responsible for the CI pipeline.

__steps:__

1. Install npm in the source directory.

1. Copy the files to the artifacts directory.

1. Publish it to Azure DevOps artifacts.

## Continuous Deployment and Continuous Delivery
For the CI/CD I've created a pipeline which using Ansible to deploy the artifacts to the environments.

>*The whole process of deployment to the Staging environment is completely automated while deployment process to the Production environment arequires an approval*

For convenience, I've imported this repository to Azure Repos and used it in the pipeline as an artifact which allows me to run this Ansible playbook on any machine(On which Asible is installed).

**The CD pipline in Azure DevOps:**

![pipeline](https://user-images.githubusercontent.com/90269123/140613014-f0d60630-fc66-4de4-80c6-2fdeef441677.JPG)


As you can see, once a new artifact added to Azure DevOps Artifacts it triggers the CD to the Staging enviroment.

**Stages Configuration:**

The Staging deployment stage is fully automatic and is triggered when there is a new artifact of Bootcamp Application.(link below)


__example:__


![stage](https://user-images.githubusercontent.com/90269123/140613158-2e05a98e-5512-4521-b1f0-2d3ae6592221.jpg)


The Production deployment stage is activated when a user with permissions approves the deployment after a successful deployment in the Staging environment.
In addition, the artifact that are deployed on the environment are exactly the same as the files that were deployed in the previous stage.(when the pipeline runs, the files that were on the Agent are not deleted)


![prod](https://user-images.githubusercontent.com/90269123/140613217-74905c8e-0977-4947-928e-f5d3e6dc5557.jpg)


>Note: Ive linked to each pipeline(stage and prod) a variable groups from the library and passing them in the command line as extra vars and using them to fill the .env file variables.
some of them contain sensitive information and are therefore not exposed to all.


![ex](https://user-images.githubusercontent.com/90269123/140613480-b0db76bc-91ec-49bc-bccf-d921cae55883.jpg)


![link](https://user-images.githubusercontent.com/90269123/140613274-4432e8ba-0b59-4d15-b6bb-66bb39650d35.jpg)






