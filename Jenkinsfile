pipeline {
    agent any

    stages {
        stage('Unitest-Manulife') {
            steps {
                echo 'get the code from github repository..'
                git branch: 'dev', credentialsId: 'Github', url: 'https://github.com/RatihNurmalasari/m-insurance-service.git'
                sh '/usr/share/maven/bin/mvn clean site'
                sh '''cd target/site
                sed -i -e \'s/<\\/head>/<link rel="stylesheet" href=".\\/css\\/maven-base.css" type="text\\/css"><link rel="stylesheet" href=".\\/css\\/maven-theme.css" type="text\\/css"><link rel="stylesheet" href=".\\/css\\/site.css" type="text\\/css"><\\/head>/\' surefire-report.html'''
                
                emailext body: '$DEFAULT_CONTENT', replyTo: '$DEFAULT_REPLYTO', subject: '$DEFAULT_SUBJECT', to: 'aryo.kusumo@photoninfotech.net'
            }
        }
        stage('Build-deploy-service') {
            steps {
                echo 'get the code from github repository..'
                git branch: 'dev', credentialsId: 'Github', url: 'https://github.com/RatihNurmalasari/m-insurance-service.git'
                
                //to add sshpass package and copy buildservice.sh file
                sh '''apk add "sshpass"
                sshpass -p \'123456\' scp /var/jenkins_home/workspace/test/buildservice.sh suryothiono_w@172.17.10.213:/home/suryothiono_w'''
                
                //to execute commands over ssh on remote host which is written in buildservice.sh file
                sh 'sshpass -p \'123456\' ssh suryothiono_w@172.17.10.213 < buildservice.sh'
                
                // For echo environmental variables BUILD_ID
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
    }
}
