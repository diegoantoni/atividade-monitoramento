pipeline{
    agent any
    environment {
        NAME_APP = "juice-shop"
        PORT_APP = "3033"
    }
    
    stages {
        stage('Build da imagem'){
            agent { node 'teste' }
            steps {
                git url: 'https://github.com/juice-shop/juice-shop'
                script {
                    docker.build "$NAME_APP:latest"
                }
            }
        }

        
        stage('Executando Container'){
            agent { node 'teste' }
            steps {
                sh '''
                    if [ ! "$(curl -s localhost:$PORT_APP &> /dev/null)" ]; then
                    docker run -d --name $NAME_APP -p $PORT_APP:3000 $NAME_APP:latest
                    fi
                '''
            } 
        }
    }

}
