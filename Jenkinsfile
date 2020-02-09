pipeline {
  agent {
    kubernetes {
      label 'jenkins-slave'  // all your pods will be named with this prefix, followed by a unique id
      idleMinutes 5  // how long the pod will live after no jobs have run on it
    }
  }
  parameters {
        string(name: 'GoodGitHash', defaultValue: 'Required', description: 'Last good git hash')
        string(name: 'BadGitHash', defaultValue: 'Required', description: 'Known bad git hash')
        string(name: 'CommandToRun', defaultValue: 'Required', description: 'Command To Run to Verify Health')
    }
  stages {
    stage('Initialize Git Bisect') {
      steps {
        echo 'Initializing Git Bisect'
        sh 'git bisect start'
        sh 'git bisect good "${GoodGitHash}"'
        sh 'git bisect bad "${BadGitHash}"'
      }
    }

    stage('Run Command') {
      steps {
        sh 'git bisect run "${CommandToRun}"'
      }
    }
  }
  post {
        always {
            deleteDir()
        }
    }
}
