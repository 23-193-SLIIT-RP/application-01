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
//         }		
//       }
//   }
// }

pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage('git repo') {
            steps {
                bat "ls -a"
                bat "rm -rf hello-world-sample-project-lolc"
                bat "git clone https://github.com/isurupathumherath/hello-world-sample-project-lolc.git"
            }
        }
        stage('clean') {
            steps {
                bat "mvn clean -f hello-world-sample-project-lolc"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f hello-world-sample-project-lolc"
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f hello-world-sample-project-lolc"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f hello-world-sample-project-lolc"
            }
        }
    }
}