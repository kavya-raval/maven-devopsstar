pipeline {
    agent any
    tools{
        maven 'maven3'
        jdk 'java'
    }
    stages {
        stage('Download code from git') {
            steps {

                echo "Downloading code from git."
                git branch: 'main', url: 'https://github.com/kavya-raval/maven-devopsstar.git'
            }
        }
        stage('Build') {
            steps {
               echo"doing Building"
               sh 'mvn clean package'
            }
        }
        stage('Archieve Artifacts') {
            steps {
                echo "archieving .war/.ear files"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Build Other Projects') {
            steps {
                echo "Send code to other job to build that project."
                build wait: false, job: 'job2-deploy-to-dev-pipeline'
            }

        }
        stage('testing') {
            steps {
                echo "Test case"
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
            }

        }
        
    }
}
