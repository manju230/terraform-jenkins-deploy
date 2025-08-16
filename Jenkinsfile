pipeline {
   agent any
   environment {
       AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
       AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
       AWS_DEFAULT_REGION    = "ap-south-1"
   }
   stages {
       stage('Terraform Init') {
           steps {
               sh '''
                   terraform init
               '''
           }
       }
       stage('Terraform Plan') {
           steps {
               sh '''
                   terraform plan -out=tfplan
               '''
           }
       }
       stage('Approval to Apply') {
           steps {
               script {
                   def userInput = input(
                       id: 'Proceed1',
                       message: 'Do you want to apply these Terraform changes?',
                       parameters: [
                           choice(name: 'CONFIRM', choices: 'NO\nYES', description: 'Select YES to continue')
                       ]
                   )
                   if (userInput == 'YES') {
                       sh 'terraform apply -auto-approve tfplan'
                   } else {
                       echo "User chose not to apply. Exiting."
                   }
               }
           }
       }
   }
}
