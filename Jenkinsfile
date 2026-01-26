pipeline {
    agent any

    tools {
        // Este nombre DEBE coincidir con el que pusiste en "Global Tool Configuration"
        maven 'maven2' 
    }

    stages {
        stage('Compilar y Empaquetar') {
            steps {
                // Ejecuta Maven para limpiar, compilar tests y crear el .war
                sh 'mvn clean package'
            }
        }

        stage('Desplegar en Tomcat') {
            steps {
                // Copia el .war generado desde la carpeta 'target' a la carpeta compartida
                // Renombramos a 'CalculadoraWeb.war' para que la URL sea limpia
                sh 'cp target/CalculadoraWeb-1.0-SNAPSHOT.war /var/jenkins_home/tomcat-deploy/CalculadoraWeb.war'
            }
        }
    }
}
