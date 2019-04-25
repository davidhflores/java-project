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
}
