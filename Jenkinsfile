pipeline {
   agent any
   environment {
       // use the Jenkins credential IDs you created
       AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
       AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
       AWS_DEFAULT_REGION    = 'ap-south-1'   // update region
   }
   stages {
       stage('Terraform Init') {
           steps {
               sh '''
                 cd ${WORKSPACE}
                 terraform init
               '''
           }
       }
       stage('Terraform Plan') {
           steps {
               sh '''
                 cd ${WORKSPACE}
                 terraform plan -out=tfplan
               '''
           }
       }
       stage('Terraform Apply') {
           steps {
               input message: "Do you want to apply these changes?"
               sh '''
                 cd ${WORKSPACE}
                 terraform apply -auto-approve tfplan
               '''
           }
       }
   }
}
