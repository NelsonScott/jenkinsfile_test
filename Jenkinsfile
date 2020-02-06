pipeline {
  agent any
  triggers {
        githubPush()
      }
  stages {
    stage('Initialize Git Bisect') {
      steps {
        echo 'Initializing Git Bisect'
        sh 'git bisect start'
        sh 'git bisect good "${GoodGitHash}"'
        sh 'git bisect bad "${params.BadGitHash}"'
      }
    }

    stage('Run Command') {
      steps {
        sh 'git bisect run "${params.CommandToRun}"'
        echo 'Running "${params.CommandToRun}"'
      }
    }

  }
}
