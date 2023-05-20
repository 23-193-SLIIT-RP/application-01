pipeline {
    agent {
      any {
        defaultContainer 'maven'
        yamlFile 'KubernetesPodJava.yaml'
      }
    }
    environment {
      DOCKER_REGISTRY_CREDS = credentials('AZURE_CONTAINER_REGISTRY')
    }
    stages {
      stage("Build & Push") {
        steps {
          container('kaniko') {
            echo "DONE"
            // echo "${env.GIT_COMMIT}"
            // script {
            //   gitCommit = "${env.GIT_COMMIT}"
            // }
            // echo "${gitCommit}"
            //  sh "/kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --build-arg GIT_COMMIT=$gitCommit --build-arg ARTIFACT=target/spring-boot-hello-world-lolc.jar --label org.opencontainers.image.revision=$gitCommit --destination=sharedregistry23.azurecr.io/$app_name:dev"
          }
        }		
      }
  }
}
