pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    build job: 'PES1UG21CS064-1', wait: true
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    def lastBuild = jenkins.model.Jenkins.instance.getItemByFullName('PES1UG21CS064-1').getLastBuild()
                    
                    if (lastBuild) {
                        def consoleOutput = lastBuild.getLog()
                        
                        echo consoleOutput
                    } else {
                        echo 'No builds found for PES1UG21CS064-1 project'
                    }
                }
            }
        }
    }
    
    post {
        always {
            script {
                if (currentBuild.result == 'FAILURE') {
                    echo 'Pipeline failed'
                }
            }
        }
    }
}