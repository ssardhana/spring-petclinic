pipeline{
    agent {label 'JDK-17'}
    options {
        timeout(time: 30, unit: 'MINUTES') 
    }
    triggers { pollSCM('* * * * *') }
    tools {
        jdk 'JDK_17' 
    }
    stages{
        stage('vcs'){
            steps{
                git url: 'https://github.com/ssardhana/spring-petclinic.git',
                    branch: 'develop'
            }

        }
        stage('build and package'){
            steps{
                sh script: 'mvn package'        
            }
        }
        stage('reporting'){
            steps{
                archiveArtifacts artifacts: '**/targets/springpetclinic-*.jar'
                junit testResults: '**/targets/surefire-reports/TEST-*.xml'
            }
        }
    }
}