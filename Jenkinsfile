node {
        
        stage('Code Checkout'){
            git 'https://github.com/mounikamc/TestDeployment.git'
        }
        
        stage ('Install'){
           nodejs('nodejs'){
           bat  'npm install'
           echo 'Installation completed'
        
           }
        }
        
        stage ('Build'){
           nodejs('nodejs'){
           bat  'npm run build'
           echo 'Build successful'
        
           }
        }

        
       stage('Sonar Scanner Coverage') {
           nodejs('nodejs'){
            bat 'npm run sonar'
            echo 'Scan completed'
          }
        }

        stage ('Uploaded files to S3') {
                withAWS(region:'us-east-2',credentials:'aws-key') {
                 bat 'aws s3 ls'
                 s3Upload(bucket:"angular-poc-cicd", includePathPattern:'**/*', workingDir:'dist/SampleAngularProject', excludePathPattern:'**/*.svg,**/*.jpg')
                }
      }
}
