pipeline {
    agent any

        tools {
        // Specify the Maven installation configured in Jenkins
        maven 'maven'
    }


    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Package') {
            steps {
                script {
                    sh 'mvn compile quarkus:dev'
                    sh 'mvn package'
                }
            }
        }

        stage('Create Uber-Jar') {
            steps {
                script {
                    sh 'mvn package -Dquarkus.package.type=uber-jar'
                }
            }
        }

        stage('Build Native Executable') {
            steps {
                script {
                    // Use GraalVM for native executable (make sure GraalVM is installed)
                    // Uncomment the next line if you have GraalVM installed
                    // sh "${MAVEN_HOME}/bin/mvn package -Dnative"

                    // Alternatively, use native executable build in a container
                    sh 'mvn package -Dnative -Dquarkus.native.container-build=true'
                }
            }
        }
    }
}
