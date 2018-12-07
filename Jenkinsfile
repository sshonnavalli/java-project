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
        sh 'aws s3 cp  jarpath/*.jar s3://SEIS665a10Jenkins'
    }
    stage("Report") {
        echo 'report'
        // sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
    }
       
}
