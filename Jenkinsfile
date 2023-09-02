// pipeline {
//     agent {
//       kubernetes {
//         defaultContainer 'maven-11'
//         yamlFile 'KubernetesPodJava.yaml'
//       }
//     }

    
//     stages {
//         stage('package') {
//             steps {
//                 sh "mvn package"
//             }
//         }
//         stage("Push to Registry") {
//           steps {
//             container('kaniko') {
//               echo "${env.GIT_COMMIT}"
//               script {
//                 gitCommit = "${env.GIT_COMMIT}"
//               }
//               echo "${gitCommit}"
//               script {
//                     def repositoryName = sh(returnStdout: true, script: "basename -s .git ${env.GIT_URL}").trim()
//                     echo "Repository Name: ${repositoryName}"
//                     sh "/kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --build-arg GIT_COMMIT=$gitCommit --build-arg ARTIFACT=target/spring-boot-hello-world-lolc.jar --label org.opencontainers.image.revision=$gitCommit --destination=sharedregistry23.azurecr.io/$repositoryName:dev"
//               }
//             }
//         }
//       }
//     }
// }

@Library('shared-library')_

echo env.BRANCH_NAME
echo env.CHANGE_BRANCH
echo env.CHANGE_ID

if(env.BRANCH_NAME=='main') { // if push to main branch 
    javaMain{}
}else if (env.CHANGE_BRANCH != 'main' && env.CHANGE_ID != null){ // if pull request
    javaMain{}
} else{
    javaMain{} //if push to another branch 
}
