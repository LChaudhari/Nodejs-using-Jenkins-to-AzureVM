pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                sudo git 'https://github.com/LChaudhari/Nodejs-using-Jenkins-to-AzureVM.git' // Replace with your Git repository URL
            }
        }
        
        stage('Build') {
            steps {
                sudo sh 'npm install' // Assuming your Node.js app uses npm for package management
            }
        }
        
        stage('Deploy') {
            steps {
                azureDeploy(connection: 'Azure_Secrets', azureCredentialsId: 'Azure_Secrets', resourceGroup: 'lalit-test', location: 'Central India') // Replace with your Azure credentials ID, resource group, location, and template file path
            }
        }
    }
}
