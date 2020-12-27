pipeline {
    agent any
    stages {
        stage ('Compile'){
                steps {
                sh 'mvn clean compile -e'
                }
        }
        stage ('Test'){
                steps {
                sh 'mvn clean test -e'
                }
        }
        stage ('Jar'){
                steps {
                sh 'mvn clean package -e'
                }
        }
        stage ('SonarQube'){
                steps {
                withSonarQubeEnv(installationName: 'sonar'){
                sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }                    
        }
        stage ('uploadNexus'){
            step { 
                nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-nexus', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'jar', filePath: 'http://127.0.0.1:8081/repository/test-nexus/0/0/1/0.0.1/0.0.1/0.0.1-0.0.1.jar']], mavenCoordinate: [artifactId: '0.0.1', groupId: '0.0.1', packaging: 'jar', version: '0.0.1']]]
            }
        }

    }
}
