pipeline {
         agent any
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
}
