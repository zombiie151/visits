pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
        }
    stages {
        stage("build image") {
            steps {
		withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh "docker build -t zombiie151/visit:$BUILD_NUMBER ."
                    sh "docker login -u $username -p $password"
                    sh "docker push zombiie151/visit:$BUILD_NUMBER"
                }
            }
        }
        stage("deploy container"){
            steps{
                sh "docker run -d --name web$BUILD_NUMBER -p 80$BUILD_NUMBER:8080 zombiie151/visit:$BUILD_NUMBER"

            }
        }
    }
}
