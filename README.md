# Iac

This Repo is to provision the AWS resources using jenkins
Steps taken:
1. Integrate the terraform with jenkins
2. MangeJenkins --> Tools --> Add terrafrom path
3. In this repo, you can pass your custom access key and secrete key as jenkins credentials, Those Jenkins Credentials can be mapped in environment section       with credentials ID.
4. This repo consists of 3 files as of now, provider.tf - inwhich you can define what cloud provider you can use, main.tf - in which we keep all the resources    config.
5. Let jus say if we want to create another resources, fork this repo and add all your tf files and add varaibles in variables.tf as needed.



Thank you
