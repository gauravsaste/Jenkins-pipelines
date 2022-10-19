pipeline {
         agent any
         environment {
              CREDS_ID = 'My Project 70142'
              BUCKET = 'jenkins-logs-bucket'
              PATTERN = "${currentBuild.number}.txt"
              //JENKINS_BUILD_URL = "${BUILD_URL}".toLowerCase
              //JENKINS_BUILD_URL = "https://tempjenkins:8080/Testjob/gs/45"
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
                         //sh 'ls'
                         println(env.PATTERN)
                         sh 'exit 1'
                         
                 }
                 }
}
        post {
           always {
             script {
               //sh 'touch joblognew1.txt'
               //sh 'echo testing >> joblognew1.txt'
               
                 if ("${BUILD_URL}".contains('%20')){
                     buildUrl = "${BUILD_URL}".replaceAll('%20',' ')
                     }
                 else{
                     buildUrl = "${BUILD_URL}"
                     }

               println(buildUrl)
               jobPath = buildUrl.split(":8080/")[1]
               println(jobPath)
               def logContent = new ByteArrayOutputStream()
               currentBuild.rawBuild.getLogText().writeLogTo(0, logContent)
               channel = build.workspace.channel;
               fp = new FilePath(channel, build.workspace.toString() + "/testing.txt")
               //File logFile = new File("${env.WORKSPACE}/${env.PATTERN}")
               fp.append(logContent.toString())
             }
               echo "Uploading job logs ${env.PATTERN} to storage bucket path: ${env.BUCKET}/$jobPath"
               googleStorageUpload bucket: "gs://${env.BUCKET}/$jobPath", credentialsId: env.CREDS_ID, pattern: "${env.PATTERN}"
           }
        }
}
