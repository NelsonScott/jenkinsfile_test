pipeline {
  agent any
  parameters {
        string(name: 'BadGitHash',
          defaultValue: '--Required--',
          description: 'A known bad Hash')
        string(name: 'GoodGitHash',
          defaultValue: '--Required--',
          description: 'A known good Hash')
        string(name: 'CommandToRun',
          defaultValue: '--Required--',
          description: 'The CMD to run to Verify Success/Failure')
    }
  stages {
    stage('Initialize Git Bisect') {
      steps {
        echo 'Initializing Git Bisect'
        sh 'git bisect start'
        sh 'git bisect good "${params.GoodGitHash}"'
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
