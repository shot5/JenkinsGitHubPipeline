pipeline {
     agent any
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MVN_HOME"
    } 
    stages {
        stage('Static Analysis') {
            steps {
                echo 'Run the static analysis to the code' 
            }
        }
        stage('Compile') {
            steps {
                echo 'Compile the source code'
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Security Check') {
            steps {
                echo 'Run the security check against the application' 
            }
        }
        stage('Run Unit Tests') {
            steps {
                echo 'Run unit tests from the source code' 
            }
        }
        stage('Run Integration Tests') {
            steps {
                echo 'Run only crucial integration tests from the source code' 
            }
        }
        stage('Publish Artifacts') {
            steps {
                //input("Do you want to continue or not?")
                echo 'Save the assemblies generated from the compilation'
                 deploy adapters: [tomcat9(credentialsId: '96c004d6-28c0-4dd5-a177-84a8c3eca199', path: '', url: 'http://localhost:8088')], contextPath: 'sample app', war: '**/*.war'
            }
        }
    }
}
