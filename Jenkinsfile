pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    stages {
        stage('Tests') {
            steps {
                sh './mvnw clean test'
            }
        }
        stage('Package') {
            steps {
                sh '''
                      ./mvnw package -DskipTests \
                      -Dquarkus.package.type=uber-jar
                 '''
                 archiveArtifacts 'target/*.jar'
            }
        }
        stage('Build Image') {
            environment { QUAY = credentials('QUAY_USER') }
            steps {
                sh '''
                   ./mvnw quarkus:add-extension \
                   -Dextensions="kubernetes,container-image-jib
                '''
            }
        }
    }
}