pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                script {
                    startZap(host: "127.0.0.1", port: 8089, timeout:300, zapHome: "/usr/local/bin/ZAP_2.7.0", allowedHosts:['http://www.agriculture.gov.ma/pages/le-ministre'], filename: "zapreport.html") // Start ZAP at /opt/zaproxy/zap.sh, allowing scans on github.com (if allowedHosts is not provided, any local addresses will be used
                }
            }
        }
        stage('attack')
        {
            steps{
            runZapAttack(userId: 1, scanPolicyName:"")
                }
        }
    }
    post {
        always {
            script {
                archiveZap(failAllAlerts: 1, failHighAlerts: 0, failMediumAlerts: 0, failLowAlerts: 0, falsePositivesFilePath: "zapFalsePositives.json")
            }
        }
    }
}
