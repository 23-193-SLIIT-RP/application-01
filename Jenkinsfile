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

pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage('git repo') {
            steps {
                sh "ls -a"
                sh "rm -rf hello-world-sample-project-lolc"
                sh "git clone https://github.com/23-193-SLIIT-RP/application-01.git"
            }
        }
        stage('clean') {
            steps {
                sh "mvn clean -f hello-world-sample-project-lolc"
            }
        }
        stage('install') {
            steps {
                sh "mvn install -f hello-world-sample-project-lolc"
            }
        }
        stage('test') {
            steps {
                sh "mvn test -f hello-world-sample-project-lolc"
            }
        }
        stage('package') {
            steps {
                sh "mvn package -f hello-world-sample-project-lolc"
            }
        }
    }
}