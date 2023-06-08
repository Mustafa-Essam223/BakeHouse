pipeline {
    agent { label 'myAgent0' }
    parameters {
        choice(name: 'ENV', choices: ['dev', 'test', 'prod',"release"])
    } 
    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
                    if (params.ENV == "release") {
                        withCredentials([usernamePassword(credentialsId: 'DockerHub-Account', usernameVariable: 'MustafaEssam', passwordVariable: 'DockerHub123456')]) {
                            sh '''
                                docker login -u ${MustafaEssam} -p ${DockerHub123456}
                                docker build -t mustafaessam/BAKEHouse:v${BUILD_NUMBER} .
                                docker push mustafaessam/BAKEHouse:v${BUILD_NUMBER}
                                echo ${BUILD_NUMBER} > ../build.txt
                            '''
                        }
                    }
                    else {
                        echo "user choosed ${params.ENV}"
                    }
                }
            }
        }
    }
}
