node {
    checkout scm
    withDockerContainer(image: 'maven:3.9.0', args: '-v /root/.m2:/root/.m2'){
    stage('Build') {
    sh 'mvn -B -DskipTests clean package'   
    }
    stage('Test') {
    sh 'mvn test'
    junit 'target/surefire-reports/*.xml'
    }
    stage('Manual Approval') {
    input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk mengakhiri)'
    }
    stage('Deploy') {
    sh './jenkins/scripts/deliver.sh'
    sleep 60s
    }
  }
}
