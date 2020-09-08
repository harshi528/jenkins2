currentBuild.displayName="jenkinstest-#"+currentBuild.number
pipeline{
    agent any 
    stages{
        stage("checkout-SCM"){
            steps{
                checkout([$class: 'GitSCM',
                branches: [[name: '*/master']],
                doGenerateSubmoduleConfigurations: false,
                extensions: [],
                submoduleCfg: [], 
                userRemoteConfigs: [[credentialsId: 'github_credentials2',
                url: 'https://github.com/HariReddy910/caramelIT.git']]])
                echo "Download finished form SCM"
            }
        }
        stage("Building"){
            steps{
                sh 'mvn -v'
                sh label: '', script: 'mvn package'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage("Deployment-AppServer"){
            steps{
              echo "hi"
             sh label: '', script: 'scp /var/lib/jenkins/workspace/CARAMELIT/target/app.war ubuntu@172.31.41.179:/home/ubuntu/appserver/webapps/caramelit2.0.war'
           }
        }
    }
}
