properties([disableConcurrentBuilds()])
pipeline {
    agent{
        label 'docker'  
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr:'10'))
        timestamps()
    }
    stages {
        stage('Build') {
            steps {
                echo "create docker image $BUILD_NUMBER "
                dir ('./'){
                    sh 'docker build -t dmachine:0.$BUILD_NUMBER . '
                }
                
            }
        }
        stage('Run') {
            steps {
                echo "Deploing ..."
                sh '(if [[-n $(docker ps | grep dmachine)]]; then docker stop dmachine && docker rm dmachine; fi)'
                sh 'docker run -d --name dmachine -p 8084:8084 dmachine:0.$BUILD_NUMBER'                               
            }
        }
    }
}
