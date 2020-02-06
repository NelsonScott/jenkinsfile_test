pipeline {
  agent any
  triggers {
        githubPush()
      }
  parameters {
        string(name: 'GoodGitHash', defaultValue: 'Required', description: 'Last good git hash')
        string(name: 'BadGitHash', defaultValue: 'Required', description: 'Known bad git hash')
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
