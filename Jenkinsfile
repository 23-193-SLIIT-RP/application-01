// pipeline {
//     agent {
//       any {
//         defaultContainer 'maven'
//         yamlFile 'KubernetesPodJava.yaml'
//       }
//     }
//     environment {
//       DOCKER_REGISTRY_CREDS = credentials('AZURE_CONTAINER_REGISTRY')
//     }
//     stages {
//       stage("Build & Push") {
//         steps {
//           container('kaniko') {
//             echo "DONE"
//             // echo "${env.GIT_COMMIT}"
//             // script {
//             //   gitCommit = "${env.GIT_COMMIT}"
//             // }
//             // echo "${gitCommit}"
//             //  sh "/kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --build-arg GIT_COMMIT=$gitCommit --build-arg ARTIFACT=target/spring-boot-hello-world-lolc.jar --label org.opencontainers.image.revision=$gitCommit --destination=sharedregistry23.azurecr.io/$app_name:dev"
//           }
//       }
//   }
// }

def call(body) {
  // evaluate the body block, and collect configuration into the object
  def pipelineParams = [: ]
  body.resolveStrategy = Closure.DELEGATE_FIRST
  body.delegate = pipelineParams
  body()

  def jobnameparts = JOB_NAME.tokenize('/') as String[]
  def app_name = jobnameparts[0]
  def gitCommit = 'UNKNOWN'

  pipeline {
      agent {
        kubernetes {
          defaultContainer 'maven-11'
          yamlFile 'KubernetesPodJava.yaml'
        }
      }
      stages {
          // stage('git repo') {
          //     steps {
          //         sh "ls -a"
          //         sh "rm -rf application-01"
          //         sh "git clone https://github.com/23-193-SLIIT-RP/application-01.git"
          //     }
          // }
          // stage('clean') {
          //     steps {
          //         sh "mvn clean"
          //     }
          // }
          // stage('install') {
          //     steps {
          //         sh "mvn install"
          //     }
          // }
          // stage('test') {
          //     steps {
          //         sh "mvn test"
          //     }
          // }
          // stage('package') {
          //     steps {
          //         sh "mvn package"
          //     }
          // }
          stage("Build & Push") {
            steps {
              container('kaniko') {
                echo "DONE"
                echo "${env.GIT_COMMIT}"
                script {
                  gitCommit = "${env.GIT_COMMIT}"
                }
                echo "${gitCommit}"
                sh "/kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --build-arg GIT_COMMIT=$gitCommit --build-arg ARTIFACT=target/spring-boot-hello-world-lolc.jar --label org.opencontainers.image.revision=$gitCommit --destination=sharedregistry23.azurecr.io/$app_name:dev"
              }
          }
        }
      }
  }
}