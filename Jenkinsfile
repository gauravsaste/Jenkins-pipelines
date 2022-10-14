pipeline {
         agent any
         environment {
              CREDS_ID = 'My Project 70142'
              BUCKET = 'jenkins-logs-bucket'
              PATTERN = '${currentBuild.number}'
         }   
         stages { 
                 stage('One') { 
                 steps {
                     echo 'Hi, this is Gaurav' 
                 }
                 }
                 stage('Two') { 
                 when { 
                       not { 
                            branch "master" 
                       } 
                 } 
                 steps {
                         echo "some build data"
                         sh 'ls'
                         println(env.PATTERN)
                         //sh 'exit 1'
                         
                 }
                 }
}
        post {
           always {
             script {
               //sh 'touch joblognew1.txt'
               //sh 'echo testing >> joblognew1.txt'
               def logContent = new ByteArrayOutputStream()
               currentBuild.rawBuild.getLogText().writeLogTo(0, logContent)
               File logFile = new File("${env.WORKSPACE}/${env.BUILD_NUMBER}.txt")
               logFile.append(logContent.toString())
               //writeFile(file: "joblog.txt", text: "joblognew1.txt")
               //sh 'sleep 50'          
               echo " build number is ${currentBuild.number}"
               //googleStorageUpload bucket: "gs://${env.BUCKET}", credentialsId: env.CREDS_ID, pattern: ${env.BUILD_NUMBER}
               //step([$class: 'StdoutUploadStep', credentialsId: env.CREDS_ID, bucket: "gs://${env.BUCKET}", logName: env.BUILD_NUMBER])
             }
               //googleStorageUpload bucket: "gs://${env.BUCKET}", credentialsId: env.CREDS_ID, pattern: env.
           }
        }
}
