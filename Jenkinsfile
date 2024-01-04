pipeline {
  agent {
    node {
      label "workstation"
    }
  }

  options {
    ansiColor('xterm')
  }

  parameters {
    choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Choose TF Action')
  }

  stages {

    stage('TF Action') {
      parallel {

        stage('DEV Env') {
          steps {
            sh 'terraform init -backend-config=env-dev/state.tfvars'
            sh 'terraform ${ACTION} -auto-approve -var-file=env-dev/main.tfvars'
          }
        }

        stage('PROD Env') {
          steps {
            sh 'terraform init -backend-config=env-prod/state.tfvars'
            sh 'terraform ${ACTION} -auto-approve -var-file=env-prod/main.tfvars'
          }
        }

      }


    }

  }

}
