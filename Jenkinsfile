pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Scardigno1982/mi_app_clima.git'
        IMAGE_NAME = 'sergioscardigno82/mi_app_clima'
        IMAGE_TAG = '12' // Se puede ajustar esto según la version
    }

    stages {
        stage('Preparar y actualizar repositorio') {
            steps {
                sh "git reset --hard HEAD"
                sh "git clean -fd"
                sh "git pull ${REPO_URL}"
            }
        }

        stage('Construcción y Etiquetado') {
            steps {
                sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
            }
        }

        stage('Ejecutar contenedor') {
            steps {
                sh "docker run --name my-container-name -d -p 3000:3000 $IMAGE_NAME:$IMAGE_TAG"
            }
        }

        stage('Pruebas') {
            steps {
                // Estoy haciendo un simple curl al servicio en el puerto 3000. Para verificar si funciona.
                sh "curl localhost:3000"
            }
        }

        stage('Publicar en DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHubCredentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    // Tu código aquí, usando las variables DOCKER_USERNAME y DOCKER_PASSWORD
                }

                sh "docker push $IMAGE_NAME:$IMAGE_TAG"
            }
        }
    }
    post {
        always {
            sh "docker rm -f my-container-name || true"
        }
    }
}
