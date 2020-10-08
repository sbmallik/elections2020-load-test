pipeline {
  agent any

  stages {
    stage ('execute tests - docker') {
      steps {
        script {
          withVaultCredentials([[path: 'secret/quality-engineering//gcp/production/service-accounts/api-services-faas-artillery', keys: ['key': 'FAAS_ARTILLERY_API_KEY']]]) {
            sh """
              docker pull quay.io/gannett/faas-artillery:latest
              docker run \
              --rm \
              -v "${pwd()}/keys:/keys" \
              -v "${pwd()}/test:/test" \
              -e FAAS_ARTILLERY_KEY=$FAAS_ARTILLERY_API_KEY \
              quality-eng-docker-artifactory.gannettdigital.com/faas-artillery:latest run \
              -c ${pwd()}/sample-artillery-config.yaml \
              -d ${pwd()}/tests
            """
          }
        }
      }
    }
  }
}