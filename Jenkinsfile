pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        TF_VAR_region = 'us-east-1'
        TF_VAR_vpc_cidr_block = '10.0.0.0/16'
        TF_VAR_subnet_cidr_blocks = '["10.0.1.0/24", "10.0.2.0/24"]'
        TF_VAR_availability_zones = '["us-east-1a", "us-east-1b"]'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/AdityaBrahmaSaiNarra/Iac.git'
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                script {
                    sh 'terraform plan -var="aws_access_key=${AWS_ACCESS_KEY_ID}" -var="aws_secret_key=${AWS_SECRET_ACCESS_KEY}" -var="region=${TF_VAR_region}" -var="vpc_cidr_block=${TF_VAR_vpc_cidr_block}" -var="subnet_cidr_blocks=${TF_VAR_subnet_cidr_blocks}" -var="availability_zones=${TF_VAR_availability_zones}"'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                script {
                    def userInput = input(
                        message: 'Do you want to run Terraform apply? Select "Proceed" to apply changes, or "Abort" to skip.',
                        parameters: [
                            choice(choices: 'Proceed\nAbort', description: 'Choose whether to proceed with Terraform apply or abort the job.', name: 'ACTION')
                        ]
                    )

                    if (userInput == 'Proceed') {
                        echo 'Running Terraform apply...'
                        sh 'terraform apply -auto-approve -var="aws_access_key=${AWS_ACCESS_KEY_ID}" -var="aws_secret_key=${AWS_SECRET_ACCESS_KEY}" -var="region=${TF_VAR_region}" -var="vpc_cidr_block=${TF_VAR_vpc_cidr_block}" -var="subnet_cidr_blocks=${TF_VAR_subnet_cidr_blocks}" -var="availability_zones=${TF_VAR_availability_zones}"'
                    } else {
                        echo 'Skipping Terraform apply.'
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                def userInput = input(
                    message: 'Do you want to run Terraform destroy? Select "Proceed" to run destroy, or "Abort" to skip.',
                    parameters: [
                        choice(choices: 'Proceed\nAbort', description: 'Choose whether to proceed with Terraform destroy or abort the job.', name: 'ACTION')
                    ]
                )

                if (userInput == 'Proceed') {
                    echo 'Running Terraform destroy...'
                    sh 'terraform destroy -auto-approve -var="aws_access_key=${AWS_ACCESS_KEY_ID}" -var="aws_secret_key=${AWS_SECRET_ACCESS_KEY}" -var="region=${TF_VAR_region}" -var="vpc_cidr_block=${TF_VAR_vpc_cidr_block}" -var="subnet_cidr_blocks=${TF_VAR_subnet_cidr_blocks}" -var="availability_zones=${TF_VAR_availability_zones}"'
                } else {
                    echo 'Skipping Terraform destroy.'
                }
            }
        }
    }
}
