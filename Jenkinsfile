pipeline {
   agent any
   stages {
       stage('Terraform Init & Plan') {
           steps {
               withAWS(credentials: 'aws-creds', region: 'ap-south-1') {
                   sh 'terraform init'
                   sh 'terraform plan -out=tfplan'
               }
           }
       }
       stage('Approval & Apply') {
           steps {
               script {
                   def userInput = input(
                       id: 'Proceed1',
                       message: 'Apply Terraform changes?',
                       parameters: [choice(name: 'CONFIRM', choices: 'NO\nYES', description: '')]
                   )
                   if (userInput == 'YES') {
                       withAWS(credentials: 'aws-creds', region: 'ap-south-1') {
                           sh 'terraform apply -auto-approve tfplan'
                       }
                   }
               }
           }
       }
   }
}
