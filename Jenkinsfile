
pipeline{
    agent any
    environment {
        NAME_APP = "api-conversao"
        PORT_APP = "8585"
        DIR_APP = "/home/jenkins/workspace/pipeline-api/src/"
    }
    
    stages {
        stage('Build da imagem'){
            agent { node 'teste' }
            steps {
                git url: 'https://github.com/diegoantoni/conversao-temperatura'
                script {
                    dir($DIR_APP){
                        docker.build "$NAME_APP:latest"
                    }
                    
                }
            }
        }

        
        stage('Executando Container'){
            agent { node 'teste' }
            steps {
                sh '''
                    if [ ! "$(curl -s localhost:$PORT_APP &> /dev/null)" ]; then
                    docker run -d --name $NAME_APP -p $PORT_APP:$PORT_APP $NAME_APP:latest
                    fi
                '''
            } 
        }
    }

}
