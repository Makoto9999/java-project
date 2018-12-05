properties([pipelineTriggers([githubPush()])])

node('linux') { 
    stage('Test') {
        git 'https://github.com/Makoto9999/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
    stage('Build') { 
        sh 'ant -f build.xml -v'
    }
    stage('Deploy') {
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://seis665-assignment10/'
    }
}
