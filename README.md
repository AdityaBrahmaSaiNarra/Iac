# Iac

This Repo is to provision the AWS resources using jenkins
Steps taken:
1. Integrate the jenkins with Terrafrom
2. In this repo, you can pass your custom access key and secrete key as jenkins credentials, Those Jenkins Credentials can be mapped in environment section with credentials ID.

NOTE: This jenkins we dont have stage to generate a terrafrom Plan and save it to a file
If you want to include terraform plan to the pipeline, please use the below code after init stage

,,,
stage("terraform plan"){
  steps{
    script{
      sh 'terrafrom plan'
    }
  }
}
'''

Thank you
