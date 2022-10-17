pipeline {
         agent any
         environment {
              CREDS_ID = 'My Project 70142'
              BUCKET = 'jenkins-logs-bucket'
              PATTERN = "${currentBuild.number}.txt"
         }   
         stages { 
                 stage('One') { 
                 steps {
                     echo 'Hi, this is Gaurav S' 
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
               //buildUrl= "$BUILD_URL".toLowerCase().replaceAll('%20',' ')
               buildUrl = "https://myjenkins:8080/Jobs/90"
                 if ($buildUrl.contains('%20')){
                     buildUrl = $buildUrl.toLowerCase().replaceAll('%20',' ')
                     }
                 else{
                     buildUrl = $buildUrl.toLowerCase()
                     }
               println(buildUrl)
               jobPath = buildUrl.split(":8080/")[1]
               println(jobPath)
               def logContent = new ByteArrayOutputStream()
               currentBuild.rawBuild.getLogText().writeLogTo(0, logContent)
               File logFile = new File("${env.WORKSPACE}/${env.PATTERN}")
               logFile.append(logContent.toString())
             }
               googleStorageUpload bucket: "gs://${env.BUCKET}/$jobPath", credentialsId: env.CREDS_ID, pattern: "${env.PATTERN}"
           }
        }
}
