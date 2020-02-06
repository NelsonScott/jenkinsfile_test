pipeline {
  agent any
  triggers {
        githubPush()
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
        echo 'Running "${CommandToRun}"'
        sh 'git bisect run "${CommandToRun}"'
      }
    }
    post {
        always {
            deleteDir()
        }
    }
  }
}
