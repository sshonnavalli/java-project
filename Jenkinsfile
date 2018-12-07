properties([pipelineTriggers([githubPush()])])
node('linux') {
    
    stage ("Unit Tests") {
        git 'https://github.com/sshonnavalli/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
    stage("Build") {
        sh 'ant -f build.xml'
    }
    stage("Deploy") {
        echo 'deploy'
    }
    stage("Report") {
        // sh "aws ec2 run-instances --image-id ami-467ca739 --count 1 --instance-type t2.micro --key-name SEIS665-demo --security-group-ids sg-0fc84e78 --region us-east-1"
       echo 'report'
    }
       
}
