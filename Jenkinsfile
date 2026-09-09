pipeline {
    agent any
    stages {
        stage('Descargar Código') {
            steps {
                checkout scm
            }
        }
        stage('Construir Frankenstein') {
            steps {
                sh 'docker build -t mi-web-frankenstein:v1 .'
            }
        }
        stage('Desplegar') {
            steps {
                echo 'Limpiando versiones anteriores y desplegando...'
                sh 'docker rm -f servidor-web || true'
                sh 'docker run -d -p 8090:80 --name servidor-web mi-web-frankenstein:v1'
            }
        }
        stage('Verificación (Smoke Test)') {
            steps {
                echo 'Comprobando que la web está viva...'
                sleep 3
                sh 'IP=$(docker inspect -f "{{.NetworkSettings.IPAddress}}" servidor-web) && curl -f http://$IP:80 || exit 1'
            }
        }
        stage('Limpiar Residuos') {
            steps {
                echo 'Eliminando imágenes huérfanas...'
                sh 'docker image prune -f'
            }
        }
    }
}
