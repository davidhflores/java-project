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
  
  stage('Deploy'){
    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS-Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
      s3Upload(includePathPattern:'*.jar', bucket:'hmk10-github-jenkins', workingDir:'dist')
    }
  }
}
