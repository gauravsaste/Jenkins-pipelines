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
                         echo "some build data" 
                 }
                 }
                 stage('Upload logs to GCS'){
                 steps{
                    script{
                         writeFile(file: 'joblog.txt', text: currentBuild.rawBuild.getLog())
                         }
                    step([$class: 'ClassicUploadStep', credentialsID: env.CREDS_ID, bucket: "gs://${env.BUCKET}", pattern: 'joblog.txt'])
                    }
                    }
                    
}
        post {
           always {
               echo 'uploading logs'
               //step([$class: 'StdoutUploadStep', credentialsId: env.CREDS_ID, bucket: "gs://${env.BUCKET}", logName: env.PATTERN])
           }
        }
}
