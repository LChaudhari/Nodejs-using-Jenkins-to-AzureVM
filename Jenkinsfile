pipeline {
  agent any

  environment {
    AZURE_CREDENTIALS = credentials('Azure_Secrets')
    AZURE_VM_IP = '20.244.119.227'
    AZURE_VM_USER = 'sampleapp'
    AZURE_VM_APP_DIR = '/var/www/app'
    GIT_REPO_URL = 'https://github.com/LChaudhari/Nodejs-using-Jenkins-to-AzureVM.git'
  }

  stages {
    stage('Deploy to Azure VM') {
      steps {
        script {
          withCredentials([azureServicePrincipal('Azure_Secrets')]) {
            def azureCredentials = AZURE_CREDENTIALS
            // SSH into the Azure VM and execute deployment steps
            sshagent(credentials: [azureCredentials]) {
              sh '''
                ssh -o StrictHostKeyChecking=no ${AZURE_VM_USER}@${AZURE_VM_IP} "
                sudo mkdir -p ${AZURE_VM_APP_DIR}
                sudo chown -R ${AZURE_VM_USER}:${AZURE_VM_USER} ${AZURE_VM_APP_DIR}
                git clone ${GIT_REPO_URL} ${AZURE_VM_APP_DIR}
                cd ${AZURE_VM_APP_DIR}
                npm install
                pm2 start index.js
                "
              '''
            }
          }
        }
      }
    }
  }
}
