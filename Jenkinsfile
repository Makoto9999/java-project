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
    stage('Report') {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '1c57667f-9fca-4e3a-ad74-b4f34660ead6', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }
    }
}
