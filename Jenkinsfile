pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    stages {
        stage('git repo & clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('install') {
            steps {
                bat 'mvn install'
            }
        }

        stage('test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('package') {
            steps {
                bat 'mvn package'
            }
        }
    }

    post {
        success {
            emailext(
                to: 'manju.sogala@gmail.com',
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build completed successfully.\n\nJob: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nBuild URL: ${env.BUILD_URL}"
            )
        }

        failure {
            emailext(
                to: 'manju.sogala@gmail.com',
                subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build failed.\n\nJob: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nBuild URL: ${env.BUILD_URL}"
            )
        }
    }
}




node {

    stage('Checkout') {
        git branch: 'main',
            url: 'https://github.com/sogalapallimanju/WEEK4-24BD1A665N-24BD1A665P-MavenJava.git'
    }

    stage('Build') {
        def mvnHome = tool 'MAVEN-HOME'

        withEnv(["PATH+MAVEN=${mvnHome}\\bin"]) {
            bat 'mvn clean package'
        }
    }

    stage('Result') {
        echo 'Maven build and tests completed successfully!'
    }

}


pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sogalapallimanju/WEEK4-24BD1A665N-24BD1A665P-MavenJava.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Result') {
            steps {
                echo 'Maven build and tests completed successfully!'
            }
        }
    }
}



