pipeline {
         agent any
         environment {
              CREDS_ID = 'My Project 70142'
              BUCKET = 'jenkins-logs-bucket'
              PATTERN = 'build-logs-test-2.txt'
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
                         //sh 'sleep 50'
                         //sh 'exit 1'
                 }
                 }
                 //stage('Upload logs to GCS'){
                 //steps{
                    //script{
                         //writeFile(file: 'joblog.txt', text: currentBuild.rawBuild.getLog())
                         //}
                    //step([$class: 'ClassicUploadStep', credentialsID: env.CREDS_ID, bucket: "gs://${env.BUCKET}", pattern: 'joblog.txt'])
                    //}
                   // }
                    
}
        post {
           always {
             script {
               //sh 'touch joblognew1.txt'
               //sh 'echo testing >> joblognew1.txt'
               writeFile(file: 'joblog.txt', text: currentBuild.rawBuild.getLog())
               sh 'sleep 50'
               googleStorageUpload bucket: "gs://${env.BUCKET}", credentialsId: env.CREDS_ID, pattern: 'joblog.txt'
               //echo 'uploading logs'
               //step([$class: 'StdoutUploadStep', credentialsId: env.CREDS_ID, bucket: "gs://${env.BUCKET}", logName: env.PATTERN])
             }
           }
        }
}
