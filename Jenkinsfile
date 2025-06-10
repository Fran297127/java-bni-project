pipeline {
    agent any
    environment {
        // Define any environment variables here
        PROJECT_NAME = "fran297127-dev"
        BUILD_NAME = "pointbreak"
    }

    stages {
        stage('Trigger Build Openshift') {
            steps {
                sh "oc start-build ${BUILD_NAME} --from-dir=. --follow -n${PROJECT_NAME}"
            }
        }
        stage('Deploy to Openshift') {
            steps {
                sh "oc rollout status dc/${BUILD_NAME} -n${PROJECT_NAME}"
            }
        }
    }

    post {
        success {
            echo 'V Build & Deploy berhasl via openshift buildconfig'
    }
        failure {
            echo 'X gagal menjalankan pipeline'
        }
    }
}