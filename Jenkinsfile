pipeline {
   agent any
   stages {
       stage('Terraform Init & Plan') {
           steps {
               withAWS(credentials: 'aws-creds', region: 'ap-south-1') {
                   sh '''
                       terraform init
                       terraform plan -out=tfplan
                   '''
               }
           }
       }
   }
}
