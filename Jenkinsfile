pipeline {
    agent any

    stages {
        stage('Descargar Código') {
            steps {
                echo 'Clonando el repositorio de GitHub...'
                checkout scm
            }
        }
        stage('Construir Frankenstein') {
            steps {
                echo 'Aquí le diremos a Docker que cocine la imagen...'
                sh 'docker build -t mi-web-frankenstein:v1 .'
            }
        }
    }
}
