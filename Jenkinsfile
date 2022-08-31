node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email adeshpande220190@gmail.com"
                        sh "git config user.name Abhijeet"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+abhidockerhub7620/argocdtest.*+abhidockerhub7620/argocdtest:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argoc-kubernetesmanifest.git HEAD:main"
                        sh "kubectl apply -f application.yml"
      }
    }
  }
}
}
