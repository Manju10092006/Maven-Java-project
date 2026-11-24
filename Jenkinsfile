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



pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    environment {
        DOCKER_IMAGE = 'sogalapallimanjunathreddy/maven-web-app:v1'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sogalapallimanju/WEEK4-24BD1A665N-24BD1A665P-MavenJava.git'
            }
        }

        stage('Clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('Install') {
            steps {
                bat 'mvn install'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
                bat 'copy /Y target\\my-maven-project-1.0-SNAPSHOT.war my-maven-project-1.0-SNAPSHOT.war'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat '''
                        echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                        docker push %DOCKER_IMAGE%
                        docker logout
                    '''
                }
            }
        }

        stage('Result') {
            steps {
                echo 'Maven build and Docker deployment completed successfully!'
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



#####Pipeline Script

pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sogalapallimanju/WEEK4-24BD1A665N-24BD1A665P-MavenJava.git'
            }
        }

        stage('Verify Project') {
            steps {
                bat 'dir'
                bat 'if not exist pom.xml (echo ERROR: pom.xml not found & exit /b 1)'
                bat 'mvn -version'
            }
        }

        stage('Clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('Build and Package') {
            steps {
                bat 'mvn -B package'
            }
        }

        stage('Verify Artifact') {
            steps {
                bat 'dir target'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Maven application built and packaged!'
        }

        failure {
            echo 'FAILURE: Check the Jenkins Console Output.'
        }
    }
}


############# ALL IN ONE JENIKINS


pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    environment {
        DOCKER_IMAGE = 'sogalapallimanjunathreddy/maven-web-app:v1'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sogalapallimanju/WEEK4-24BD1A665N-24BD1A665P-MavenJava.git'
            }
        }

        stage('Clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('Install') {
            steps {
                bat 'mvn install'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
                bat 'copy /Y target\\my-maven-project-1.0-SNAPSHOT.war my-maven-project-1.0-SNAPSHOT.war'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: '729fa482-1c81-4402-a8d2-80273aff4b5f',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat '''
                        echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                        docker push %DOCKER_IMAGE%
                        docker logout
                    '''
                }
            }
        }

        stage('Docker Deploy') {
            steps {
                bat '''
                    docker stop maven-web-app
                    docker rm maven-web-app
                    docker run -d --name maven-web-app -p 8081:8080 %DOCKER_IMAGE%
                '''
            }
        }

        stage('Result') {
            steps {
                echo 'Maven build and Docker deployment completed successfully!'
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
#############DOCKER IMAGE 

FROM tomcat:10.1-jdk17

COPY my-maven-project-1.0-SNAPSHOT.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]

ngrok config add-authtoken YOUR_AUTHTOKEN https://abc123.ngrok-free.app/github-webhook/ ngrok http 8080
