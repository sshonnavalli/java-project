properties([pipelineTriggers([githubPush()])])
node('linux') {
    
    stage ("Unit Tests") {
        git 'https://github.com/sshonnavalli/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
    stage("Build") {
        sh 'ant -f build.xml -v'
    }
    stage("Deploy") {
        sh 'echo "deploy ${JENKINS_HOME}"'
        sh 'aws s3 cp /workspace/java-pipeline/dist/*.jar s3://seis665a10bucket/'
    }
    stage("Report") {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '58b29f03-5bd3-425c-85fa-bc080f2363c8', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }
        
    }
       
}
