#!groovy

node('docker-agent-slave') {
    def nodeHome
    def workspace = pwd()

    stage('Preparation') {
        // Get some code from a GitHub repository
        //git url: 'https://github.com/thoschu/de.schulte360.npm.letter-count.git', credentialsId: 'GitHub-Admin'
        git 'https://github.com/thoschu/de.schulte360.npm.letter-count.git'
         
        // Get the NodeJS tool.
        // ** NOTE: This 'node-8-standard' NodeJS tool must be configured
        // **       in the global configuration.           
        nodeHome = tool 'node-8-standard'
        
        if (isUnix()) {
            // on linux / mac
            env.PATH="${nodeHome}/bin:${env.PATH}"
        } else {
            // on windows
            env.PATH="${nodeHome};${env.PATH}"
        }
    
        sh 'node -v'
        sh 'npm --version'

        echo "\u2600 workspace=${workspace}"
       
        sh 'touch .npmrc'
        sh 'echo ${NPMRC} > ".npmrc"'
    }
    
    stage('Install dependencies') {
        sh 'npm install'
    }
    
    stage('Unit tests') {
        sh 'npm test'
    }
    
    stage('Build') {
        sh 'npm run build'
    }
    
    stage('Results') {
        //junit '**/target/surefire-reports/TEST-*.xml'
        archive 'build/*.tgz'
    }
        
    stage('Delivery') {
        sh 'npm publish'
    }
        
    stage('Functional tests') {
        // ToDo with e.g. GEB
    }  
        
    stage('Deployment') {
        // ToDo
    }
}
