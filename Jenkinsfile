// @Library('shared-libraries@1.0.1')_

//pythonPipeline {}

// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            // Or, to avoid YAML:
            // containerTemplate {
            //     name 'shell'
            //     image 'ubuntu'
            //     command 'sleep'
            //     args 'infinity'
            // }
            yamlFile 'jenkinsPod.yaml'
            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
            defaultContainer 'shell'
            retries 2
        }
    }
    stages {
        stage('Main') {
            steps {
                container('python') {
                    sh '''
                    pip install -r requirements.txt
                    bandit -r . -x '/.venv/','/tests/'
                    black .
                    flake8 . --exclude .venv
                    pytest -v --disable-warnings
                    '''
                 }
            }
        }
    }
}