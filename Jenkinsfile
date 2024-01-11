pipeline{
    agent any
    tools{
        jdk 'jdk17'
        maven 'mvn3'
    }
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }
    
    stages{
        
        stage('git fetch'){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Sk071/vprofile-project.git'
            }
        }
        
        stage('build code'){
            steps{
                sh 'mvn clean install'
            }
            post{
                success{
                echo "Now archiving..."
                archiveArtifacts artifacts: 'target/*.war'
                }
            }
        }
        
        stage('checkstyle integration'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        
        
        
        stage('Upload Artifacts to Nexus'){
        steps{
        nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: 'yourip:8081/',
        groupId: 'QA',
        version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
        repository: 'vprofile',
        credentialsId: 'nexus',
        artifacts: [
            [artifactId: 'vprofile',
             classifier: '',
             file: 'target/vprofile-v2.war',
             type: 'war']
        ]
     )
            }
        }

 }
}
