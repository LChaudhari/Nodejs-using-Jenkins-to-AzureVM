pipeline {
  agent any

  environment {
    AZURE_VM_IP = '20.244.119.227'
    AZURE_VM_USER = 'sampleapp'
    AZURE_VM_APP_DIR = '/var/www/app'
    GIT_REPO_URL = 'https://github.com/LChaudhari/Nodejs-using-Jenkins-to-AzureVM.git'
  }

  stages {
    stage('Deploy to Azure VM') {
      steps {
        script {
          // SSH into the Azure VM and execute deployment steps
          withCredentials([sshUserPrivateKey(credentialsId: 'AzureVM_USR_PASS', keyFileVariable: 'sampleapp')]) {
            sh '''
              ssh -o StrictHostKeyChecking=no -i $SSH_KEY ${AZURE_VM_USER}@${AZURE_VM_IP} "
                sudo mkdir -p ${APP_DIR}
                sudo chown -R ${AZURE_VM_USER}:${AZURE_VM_USER} ${APP_DIR}
                git clone ${GIT_REPO_URL} ${APP_DIR}
                cd ${APP_DIR}
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
