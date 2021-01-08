 pipeline {
    agent {
      label "go"
    }
    stages {
        stage("Build release") {
            steps {
                sh "make"
            }
        }
        stage("Create release tar") {
            steps {
                sh "tar -cvzf goproxy.linux-amd64.tar.gz bin/"
            }
        }
        stage("Archive release tar") {
            steps {
                archiveArtifacts artifacts: 'goproxy.linux-amd64.tar.gz'
            }
        }
        stage("publish release tar") {
            agent {
              label "master"
            }
            steps {
                sh "mkdir -p /home/jenkins/artifacts/jobs/${JOB_NAME}/${BUILD_NUMBER}"
                sh "cp ${JENKINS_HOME}/jobs/SRE/jobs/${JOB_BASE_NAME}/builds/${BUILD_NUMBER}/archive/goproxy.linux-amd64.tar.gz ${JENKINS_HOME}/artifacts/jobs/${JOB_NAME}/${BUILD_NUMBER}/goproxy.linux-amd64.tar.gz"
            }
        }
    }
}
