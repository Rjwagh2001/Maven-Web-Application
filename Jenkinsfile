
node {

    stage('CheckoutCode Code') {
        git credentialsId: '2c49ff46-49bc-49c5-8924-ee0268231059',
            url: 'https://github.com/Rjwagh2001/Maven-Web-Application.git'
    }

    stage('SonarQube Report') {
        sh 'mvn sonar:sonar'
    }

    stage('Upload Artifact to Nexus') {
        sh 'mvn deploy'
    }

    stage('Deploy in Tomcat Server') {
        sshagent(credentials: ['TomcatServerCredentialsSSH']) {
            sh '''
                scp -o StrictHostKeyChecking=no \
                target/maven-web-application.war \
                ec2-user@13.203.101.38:/opt/tomcat9/webapps/
            '''
        }
    }
}
