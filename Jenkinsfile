pipeline {
         agent any
         environment {
              CREDS_ID = 'My Project 70142'
              BUCKET = 'jenkins-logs-bucket'
              PATTERN = 'test-build-logs.txt'
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
                         echo "Hello" 
                 }
                 }
}
        post {
           always {
               step([$class: 'StdoutUploadStep', credentialsId: env.CREDS_ID, bucket: "gs://${env.BUCKET}", logName: env.PATTERN])
           }
        }
}
