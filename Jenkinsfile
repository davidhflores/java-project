properties([pipelineTriggers([githubPush()])])

node('linux'){
  
  git'https://github.com/davidhflores/java-project.git'
  
  stage('Test'){
    sh 'ant -f test.xml -v'
    junit 'reports/result.xml'
  }
  
  stage('Build'){
    sh 'ant -f build.xml -v'
  }
  
  withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS-Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
    stage('Deploy'){
      s3Upload(includePathPattern:'*.jar', bucket:'hmk10-github-jenkins', workingDir:'dist')
    }
  
    stage('Report'){
      sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
    }
  }
}
