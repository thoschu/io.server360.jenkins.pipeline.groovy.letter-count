#!groovy

node('docker-agent-slave') {
    def nodeHome
    
    stage('Preparation') {
        // Get some code from a GitHub repository
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
        sh 'npm build'
    }
    
    stage('Results') {
        //junit '**/target/surefire-reports/TEST-*.xml'
        archive '**/*'
    }
        
    stage('Delivery') {
        // ToDo
    }
        
    stage('Functional tests') {
        // ToDo
    }  
        
    stage('Deployment') {
        // ToDo
    }
}
