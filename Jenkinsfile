@Library('shared-libraries') _

//pythonPipeline {}

// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            yamlFile 'jenkinsPod.yaml'
            
        }
    }
    stages {
        stage('JUnit test') {
            steps {
                pythonUnitTest {}
            }
        }
    }
}