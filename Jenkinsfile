properties([pipelineTriggers([githubPush()])])

node('linux') {
  stage('Test') {
    git'https://github.com/davidhflores/java-project.git'
    sh 'ant -f test.xml -v'
    junit 'reports/result.xml'
  }
}
