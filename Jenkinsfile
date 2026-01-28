pipeline {
    agent any

    tools {
        // IMPORTANTE: Debe coincidir con el nombre en "Global Tool Configuration"
        maven 'maven2'
    }

    stages {
        stage('Checkout') {
            steps {
                // Tu repositorio real y la rama 'main'
                git branch: 'main', url: 'https://github.com/MartinIESBelen/proyectoJeankins2.git'
            }
        }

        stage('Build & Compile') {
            steps {
                // Compila para asegurar que el código es válido
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                // Ejecuta los tests unitarios (JUnit)
                sh 'mvn test'
            }
        }

        stage('Package & Deploy') {
            steps {
                // Empaqueta el .war (saltando tests porque ya pasaron en la etapa anterior)
                sh 'mvn package -DskipTests'
                
                // COMANDO CLAVE DE DESPLIEGUE:
                // Toma cualquier .war generado en 'target' y lo copia al volumen compartido.
                // Lo renombramos a 'proyectoJeankins2.war' para que la URL sea /proyectoJeankins2
                sh 'cp target/*.war /var/jenkins_home/tomcat-deploy/proyectoJeankins2.war'
            }
        }
    }
    
    post {
        success {
            echo '¡Éxito! Tu app está disponible en: http://localhost:8080/proyectoJeankins2/'
        }
        failure {
            echo 'Algo falló. Revisa la consola de salida (Console Output).'
        }
    }
}
