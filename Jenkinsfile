
pipeline {
    agent any
    stages {
        stage('downloadNexus') {
         steps {    
          sh 'curl -X GET -u admin:admin http://localhost:8081/repository/test-nexus/com/devopsusach2020/DevOpsUsach2020/0.0.1/DevOpsUsach2020-0.0.1.jar -O'
          }
         }
        stage('Run') {
         steps {
	        sh 'nohup java -jar DevOpsUsach2020-0.0.1.jar &'
         }
        } 
      stage('Wait up app') {
        steps {
	      sh 'sleep 30'
       } 
      }
      stage('Testing app') {
       steps {
        sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing'
        }
       }
      stage('Result Chile') {
       steps {
        sh 'curl -X GET http://localhost:8081/rest/mscovid/estadoPais?pais=CHILE'
        }
       }
      stage('Result Mundial') {
       steps {
        sh 'curl -X GET http://localhost:8081/rest/mscovid/estadoMundial'
        }
       }  
      stage('uploadNexus') {
          steps {
          nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-nexus', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'jar', filePath: 'DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '1.0.0']]]
         } 
        }
       }
      } 
