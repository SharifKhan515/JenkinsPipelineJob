pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build the demo desclarative pipeline job'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Linux Test') {
      parallel {
        stage('Linux Test') {
          steps {
            echo 'Running Linux Test'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows Test') {
          steps {
            echo 'WIndows test running'
          }
        }

      }
    }

    stage('Deployment Staging') {
      steps {
        echo 'Deploy to staging '
        input 'Ok to depl;oyb to production'
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploying in Prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}